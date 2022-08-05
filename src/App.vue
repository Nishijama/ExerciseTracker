<template>
<div class="container">
    <Header title="exercise planner." />
    <Sessions :sessions="sessions" />
</div>
</template>

<script>
import Header from './components/Header'
import Sessions from './components/Sessions'

export default {
  name: 'App',
  components: {
    Header,
    Sessions,
  },
  data() {
    return {
      sessions: [],
    }
  },
  created() {
    this.sessions = [
      {
        id: 1,
        date: "2022-08-03",
        exercises: {
          exercise1: "Push-ups",
          exercise2: "Goblet Squats",
          exercise3: "Kettlebell Snatch",
          exercise4: "Kettlebell Halo"
        },
        sets: 3,
        reps: 10,
      },
      {
        id: 2,
        date: "2022-08-05",
        exercises: {
          exercise1: "Mountain Climbers",
          exercise2: "Kettlebell Swing",
          exercise3: "Kettlebell Row",
          exercise4: "Kettlebell Halo"
        },
        sets: 3,
        reps: 10,
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
