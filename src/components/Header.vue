<template>
    <header>
        <h1>{{ title }}</h1>
        <Button 
            @btn-click="$emit('toggle-add-session')" 
            :text="showAddSession ? 'close.' : 'new session.'" 
            :color="showAddSession ? 'palevioletred' : 'black'" />
    </header>
</template>

<script>
import Button from './Button'

export default {
    name: 'Header',
    props: {
        title: String,
        showAddSession: Boolean

    },
    components: {
        Button,
    }
}
</script>

<style scoped>
header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
}
</style>