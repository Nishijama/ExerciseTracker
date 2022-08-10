<template>
<div class="main">
    <div :key="session.id" v-for="session in sessions">
        <Session 
        @toggle-reminder="$emit('toggle-reminder', session.id)"
        @toggle-add-session="$emit('toggle-add-session')"
        @duplicate-session="$emit('duplicate-session', session)"
        @delete-session="$emit('delete-session', session.id)"
        :session="session" />
    </div>
</div>
</template>

<script>
import Session from './Session.vue'

export default {
    name: "Sessions",
    props: {
        sessions: Array,
    },
    components: { 
        Session 
    },
          emits: ['edit-session','duplicate-session', 'delete-session', 'toggle-reminder','toggle-add-session'],
}
</script>

<style scoped>
    .main {
        display: grid;
        grid-template-columns: 45% 45%;
        column-gap: 10%;
        row-gap: 30px;
    }
</style>