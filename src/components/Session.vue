<template>
    <div :class="[session.reminder ? 'reminder': '', 'session_card']">
        <div class="card_inner_div">
            <h3>{{session.date}} </h3>
            <h5>{{session.sets}} x {{session.reps}}</h5>
            <p v-for="exercise in session.exercises">{{exercise}}</p>
        </div>
        <div class="icons">
            <i @click="$emit('toggle-reminder', session.id)" class="fas fa-thin fa-bell"></i> 
            <i @click="$emit('edit-session', session.id)" class="fas fa-thin fa-edit"></i> 
            <i @click="$emit('duplicate-session', session.id)" class="fas fa-thin fa-copy"></i> 
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
        emits: ['edit-session','duplicate-session', 'delete-session', 'toggle-reminder']
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
    i {
        display: block;
        width: min-content;
    }
    .icons {
        width: 50px;
        background-color: rgb(200, 200, 200);
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }
    .reminder {
        border-top: 2px solid green;
    }
    div {
        background-color: rgb(234, 234, 234);
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        padding: 15px;
        margin: 0px;
    }
    .session_card {
        padding: 0px;
        min-height: 100%;
    }
    .card_inner_div {
        display: flex;
        flex-direction: column;
        justify-content: start;
        line-height: 200%;
    }
</style>