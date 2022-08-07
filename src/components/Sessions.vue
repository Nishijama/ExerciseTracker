<template>
<div class="main">
    <div :key="session.id" v-for="session in sessions">
        <Session 
        @delete-session="$emit('delete-session', session.id)" 
        @toggle-reminder="$emit('toggle-reminder', session.id)"
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
  emits: ['delete-session', 'toggle-reminder'],
}
</script>

<style scoped>
    .main {
        display: flex;
        flex-direction: row;
    }
</style>