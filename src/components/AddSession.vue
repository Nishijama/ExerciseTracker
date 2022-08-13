<template>
<form @submit="onSubmit" class="add-form">
    <div class="form-control">
        <input type="date" id="session_date" v-model="date" name="session_date" placeholder="date.">
    </div>
    <!-- <div class="form-control">
        <input type="number" name="sets" id="session_sets" v-model="sets" placeholder="sets.">
    </div>
    <div class="form-control">
        <input type="number" name="reps" id="session_reps" v-model="reps" placeholder="reps."> 
    </div> -->
    <div class="form-control">
        <input type="number" name="exercise_count" v-model="exercise_count" id="session_exercise_count" placeholder="number of exercises."> 
    </div>
    
    <div v-for="index in exercise_count" :exercise_count=exercise_count :key="index" class="form-control form-control-inline">
            <input type="text" class="exercise" v-model="exercises[index]['exercise']" :id="index" placeholder="exercise.">
            <input type="number" name="sets" v-model="exercises[index]['sets']" id="session_sets" placeholder="sets.">
            <input type="number" name="reps" v-model="exercises[index]['reps']" id="session_reps" placeholder="reps."> 
    </div>

    <div class="form-control form-control-check">
        <input type="checkbox" v-model="reminder" name="reminder" id="reminder">
        <label for="reminder"> Set reminder</label>
    </div>
    <input type="submit" value="Save session" class="btn btn-block">
</form>
</template>


<script>
    export default {
        name: 'AddSession',
        data() {
            return {
                date: '',
                // sets: '',
                // reps: '',
                exercise_count: '',
                exercises: [],
                reminder: false,
            }
        },
        methods: {
            onSubmit(e) {
                e.preventDefault()
                if (!this.date || !this.sets || !this.reps) {
                    alert('Please fill in the details');
                    return;
                }
                const newSession = {
                    id: Math.floor(Math.random()*100000),
                    date: this.date,
                    sets: this.sets,
                    reps: this.reps,
                    exercises: this.exercises,
                    reminder: this.reminder,
                }
                this.date = ''
                this.sets = ''
                this.reps = ''
                this.exercise_count = ''
                this.exercises = []
                this.reminder = false

                this.$emit('add-session', newSession);
                this.$emit("toggle-add-session");

            }, 
        }
    }

</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;

}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-inline input {
    width:30%;
}
.form-control-check {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: start;
}
.form-control-check label {
  padding-left: 10px;
}
.form-control-check input {
  height: 20px;
  width: 20px;
  display:block;
}
</style>