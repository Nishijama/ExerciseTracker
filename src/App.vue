<template>
<div class="container">
    <Header 
        :showAddSession="showAddSession" 
        @toggle-add-session="toggleAddSession" 
        title="exercise plan." />
    
    
    <AddSession 
        v-show="showAddSession" 
        @toggle-add-session="toggleAddSession" 
        @add-session="addSession" />

    <Sessions 
        @toggle-add-session="toggleAddSession"
        @toggle-reminder="toggleReminder"
        @edit-session="editSession"
        @duplicate-session="duplicateSession"
        @delete-session="deleteSession"
        :sessions="sessions" />
</div>
</template>

<script>
import { thisExpression, tsAnyKeyword } from '@babel/types'
import Header from './components/Header'
import Sessions from './components/Sessions'
import AddSession from './components/AddSession.vue'

export default {
  name: 'App',
  components: {
    Header,
    Sessions,
    AddSession,
},

  data() {
    return {
      sessions: [],
      showAddSession: false
    }
  },

  methods: {
    async deleteSession(id) {
        if (confirm("are you sure?")) {

          const res = await fetch(`api/sessions/${id}`, {
            method: "DELETE"
          })

          if (res.status === 200) {
            this.sessions = this.sessions.filter((session) => session.id !== id)
          } else {
            alert(`Error deleting session`)
          }
      }
    },

    async addSession(newSession) {
      console.log(JSON.stringify(newSession));
      
      const res = await fetch('api/sessions', {
        method: "POST",
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(newSession)
      })

      const data = await res.json()


      this.sessions = this.sessions.map( (session) =>
      session.id !== newSession.id ? {...session, new: false} : session)
      newSession.new = true;
      this.sessions = [...this.sessions, newSession]
    },

    editSession(id) {
      console.log("Editing session nr", id);
      // TODO
    },

    setNew(newSession) {
      this.sessions = this.sessions.map( (session) =>
        session.id !== newSession.id ? {...session, new: false} : session)
      newSession.new = true
    },

    async duplicateSession(session) {
      console.log("Duplicated session nr", session.id);

      let newSession = JSON.parse(JSON.stringify(session))
      newSession.id = this.sessions.length 
      //
      const res = await fetch('api/sessions', {
        method: "POST",
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(newSession)
      })
      
      const data = await res.json()
      //
      this.setNew(newSession)
      // this.sessions.unshift(newSession)
      this.sessions = [...this.sessions, newSession]
      console.log(this.sessions);
    },


    async toggleReminder(id) {
      const sessionToToggle = await this.fetchSession(id);
      const updatedSession = {...sessionToToggle, reminder: !sessionToToggle.reminder}

      const res = await fetch(`api/sessions/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json"
        },
        body: JSON.stringify(updatedSession)
      })
      const data = await res.json()
      console.log("reminder set for session", id);
      this.sessions = this.sessions.map( (session) =>
      session.id === id ? {...session, reminder: data.reminder} : session)
    },

    toggleAddSession() {
      this.showAddSession=!this.showAddSession;
    },

    async fetchSessions() {
      const res = await fetch('api/sessions')
      const data = await res.json()
      return data
    },
    async fetchSession(id) {
      const res = await fetch(`api/sessions/${id}`)
      const data = await res.json()
      return data
    },
  },
  async created() {
    this.sessions =  await this.fetchSessions()
  }
}

</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 800px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid black;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
