<template>
    <header>
        <h1> Task Tracker </h1>
        <Button @click="onClick()" color="green" text="Add Task" />
    </header>
</template>

<script>
import Button from './Button.vue'

export default {
    name: 'Header',
    props: {
        title: String,
    },
    components: {
        Button,
    },
    methods: {
        onClick() {
            console.log('CLicked')
        }
    }

}

</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>