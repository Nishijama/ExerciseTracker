<template>
<form @submit="onSubmit" class="add-form">
    <div class="form-control">
        <input type="date" id="session_date" v-model="date" name="session_date" placeholder="date.">
    </div>
    <div class="form-control">
        <input type="number" name="exercise_count" v-model="exercise_count" id="session_exercise_count" placeholder="number of exercises."> 
    </div>
    
    <div v-for="index in exercise_count" :exercise_count=exercise_count :key="index" class="form-control form-control-inline">
            <input type="text" name="exercise" v-model="exercises[index]" :id="'exercise'+index" placeholder="exercise.">
            <input type="number" name="sets" v-model="sets[index]" :id="'sets'+index" placeholder="sets.">
            <input type="number" name="reps" v-model="reps[index]" :id="'reps'+index" placeholder="reps."> 
    </div>

    <div class="form-control form-control-check">
        <input type="checkbox" v-model="reminder" name="reminder" id="reminder">
        <label for="reminder"> Set reminder</label>
    </div>
    <input type="submit" value="Save session" class="btn btn-block">
</form>
</template>


<script>
import { thisTypeAnnotation } from '@babel/types';

    export default {
        name: 'AddSession',
        data() {
            return {
                date: '',
                exercise_count: '',
                exercises: [],
                sets: [],
                reps: [],
                reminder: false,
                }
        },
        methods: {
            onSubmit(e) {
                e.preventDefault()

                console.log(this.exercises);
                console.log(this.sets);
                console.log(this.reps);

                if (!this.date) {
                    alert('Please fill in the details');
                    return;
                }

                let temp_exercises =[]
                for (let i=1; i<this.exercises.length; i++) {
                    let exercise_instance = {
                        exercise: this.exercises[i],
                        sets: this.sets[i],
                        reps: this.reps[i]
                    }
                    temp_exercises = [...temp_exercises, exercise_instance]
                }

                const newSession = {
                    id: Math.floor(Math.random()*100000),
                    date: this.date,
                    exercises: temp_exercises,
                    reminder: this.reminder,
                }
                this.date = ''
                this.exercises = []
                this.exercise_count = ''
                this.sets = []
                this.reps = []
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