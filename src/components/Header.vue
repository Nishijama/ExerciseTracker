<template>
    <header>
        <h1>{{ title }}</h1>
        <Button text="new session." color="palevioletred" />
    </header>
</template>

<script>
import Button from './Button'

export default {
    name: 'Header',
    props: {
        title: String,
    },
    components: {
        Button,
    }
}
</script>

<style scoped>
header {
    display: flex;
    justify-content: space-around;
    margin: 20px;
    align-items: center;
}
</style>