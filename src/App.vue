<template>
<div class="container">
    <Header title="exercise plan." />
    <AddSession @add-session="addSession" />
    <Sessions 
      @delete-session="deleteSession" 
      @toggle-reminder="toggleReminder"
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
    }
  },
  methods: {
    deleteSession(id) {
        if (confirm("are you sure?")) {
        this.sessions = this.sessions.filter((session) => session.id !== id)
      }
    },
    toggleReminder(id) {
      console.log("reminder set for session", id);
      this.sessions = this.sessions.map( (session) =>
      session.id === id ? {...session, reminder: !session.reminder} : session)
    }
  },
  created() {
    this.sessions = [
      {
        id: 1,
        date: "2022-08-03",
        exercises: ["Push-ups", "Goblet Squats", "Kettlebell Snatch", "Kettlebell Halo"],
        sets: 3,
        reps: 10,
        reminder: false,
      },
      {
        id: 2,
        date: "2022-08-05",
        exercises: [ "Mountain Climbers","Kettlebell Swing","Kettlebell Row","Kettlebell Halo"],
        sets: 3,
        reps: 10,
        reminder: true,
      },
    ]
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
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
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
