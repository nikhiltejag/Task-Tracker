<template>
    <div :key="task.id" v-for="task in tasks">
        <Task @toggle-remainder="$emit('toggle-remainder', task.id)" @delete-task="$emit('delete-task', task.id)" :task="task"/>
    </div>
</template>

<script>
import Task from './Task.vue'

export default {
    name: 'Tasks',
    props: {
        tasks: Array,
    },
    components: {
        Task
    },
    // methods: {
    //     onDelete(id){
    //         this.$emit('delete-task', id)
    //     },
    // },
    emits: ['delete-task', 'toggle-remainder'],
}
</script>

<style>
    .task {
        background-color: #f4f4f4;
        padding: 10px 20px;
        margin: 5px;
        cursor: pointer;
        text-align: left;
    }

    .remainder {
        border-left: 5px solid green;
    }

    .task h3 {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
</style>