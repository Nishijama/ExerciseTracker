<template>
<div class="main">
    <div :key="session.id" v-for="session in sessions">
        <Session :session="session" />
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
    }
}
</script>

<style scoped>
    .main {
        display: flex;
        flex-direction: row;
    }
</style>