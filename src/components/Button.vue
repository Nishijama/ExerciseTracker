<template>
    <button @click="onClick()" :style="{background: color}" class='btn'>{{ text }}</button>
</template>

<script>
    export default {
        name: 'Button',
        props: {
            text: String,
            color: String,
        },
        methods: {
            onClick() {
                console.log('click');
                fetch("https://api.ipify.org/?format=json")
                .then(response => response.json())
                .then(data => {
                    console.log(data.ip)
                    return fetch(`https://ipapi.co/${data.ip}/json/`)
                 })
                .then(response => response.json())
                .then(data => console.log(data.city, data.country))
                
            }
        },
    }
</script>
