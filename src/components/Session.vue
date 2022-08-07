<template>
    <div :class="[session.reminder ? 'reminder': '']" style="margin: 20px;">
        <h3>{{session.date}} </h3>
        <h5>{{session.sets}} x {{session.reps}}</h5>
        <p v-for="exercise in session.exercises">{{exercise}}</p>
        <div class="icons">
            <i @click="$emit('toggle-reminder', session.id)" class="fas fa-thin fa-bell"></i> 
            <i @click="$emit('delete-session', session.id)" class="fas fa-thin fa-trash"></i> 
        </div>

    </div>
</template>

<script>

    export default {
        name: "Session",
        props: {
            session: Object,
        },
        emits: ['delete-session', 'toggle-reminder']
    }
</script>

<style scoped>
    .fas {
        cursor: pointer;
    }
    .fa-trash {
        color: palevioletred;
    }
    .fa-bell {
        color: green;
    }
    .icons {
        margin:10px 0px;
        padding:0px;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }
    .reminder {
        border-top: 2px solid green;
    }
    div {
        background-color: rgb(234, 234, 234);
        padding: 15px;
        margin: 20px;
    }
</style>