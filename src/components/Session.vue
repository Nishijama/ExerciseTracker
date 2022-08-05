<template>
    <div style="margin: 20px;">
        <h3>{{session.date}}</h3>
        <h5>{{session.sets}} x {{session.reps}}</h5>
        <p>{{session.exercises.exercise1}}</p>
        <p>{{session.exercises.exercise2}}</p>
        <p>{{session.exercises.exercise3}}</p>
        <p>{{session.exercises.exercise4}}</p>
    </div>
</template>

<script>

    export default {
        name: "Session",
        props: {
            session: Object,
        },
    }
</script>

<style scoped>
    div {
        background-color: rgb(234, 234, 234);
        padding: 15px;
        margin: 20px;
    }
</style>