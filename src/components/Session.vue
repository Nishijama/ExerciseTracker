<template>
    <div :class="[session.reminder ? 'reminder': '', session.new ? 'new': '', 'session_card']">
        <div class="card_inner_div">
            <h3>{{session.date}} </h3>
            <!-- <h5>{{session.sets}} x {{session.reps}}</h5> -->
            <div v-for="exercise in session.exercises">
                <p>{{exercise.exercise}}</p>
                <p style="padding-left: 20px;">{{exercise.sets}} x {{exercise.reps}}</p>
            </div>
        </div>
        <div class="icons">
            <i @click="$emit('toggle-reminder', session.id)" class="fas fa-thin fa-bell"></i> 
            <i @click="editSession()" class="fas fa-thin fa-edit"></i> 
            <i @click="$emit('duplicate-session', session)" class="fas fa-thin fa-copy"></i> 
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
        methods:{
            editSession(session) {
                console.log("hello");
                this.$emit("toggle-add-session");
            },
        },
        emits: ['edit-session','duplicate-session', 'delete-session', 'toggle-reminder', 'toggle-add-session']
    }
</script>

<style scoped>
    @keyframes fade {
    from {opacity: 100%;}
    to {opacity: 0%;}
    }

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
        margin:10px 0px;
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
    .new {
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(5, 197, 255, 0.691);
        animation-name: fade;
        animation-duration: 1s;
        animation-direction: reverse;

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