<template>
<form @submit="onSubmit" class="add-form">
    <div class="form-control">
        <input type="date" id="session_date" v-model="date" name="session_date" placeholder="date.">
    </div>
    <div class="form-control">
        <input type="number" name="sets" id="session_sets" v-model="sets" placeholder="sets.">
    </div>
    <div class="form-control">
        <input type="number" name="reps" id="session_reps" v-model="reps" placeholder="reps."> 
    </div>
    <div class="form-control">
        <input type="number" name="exercise_count" v-model="exercise_count" id="session_exercise_count" placeholder="number of exercises."> 
    </div>
    <div class="form-control" v-for="index in exercise_count" :exercise_count=exercise_count :key="index">
        <input type="text" class="exercise" :id="index" :placeholder="index">
    </div>
    <div class="form-control form-control-check">
        <label for="reminder"> Set reminder</label>
        <input type="checkbox" v-model="reminder" name="reminder" id="reminder">
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
                sets: '',
                reps: '',
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
                // const exercise_list = document.querySelectorAll('.exercise');
                

                // exercise_list.forEach(exercise => {
                //     alert(exercise)
                //     this.exercises.push(exercise)
                // });
                // alert(this.exercises)

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
                this.reminder = false

                this.$emit('add-session', newSession);
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
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>