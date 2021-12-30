<template>
    <div @dblclick="$emit('toggle-remainder', task.id)" :class="[task.remainder?'remainder': '', 'task']">
        <h3>{{task.text}}
            <span @click="$emit('delete-task', task.id)" class="cross">X</span>
        </h3>
        <p>{{task.day}}</p>
    </div>

</template>

<script>
export default {
    name: 'Task',
    props: {
        task: Object,
    },
   
}
</script>

<style scope>
    .cross {
        color: red;
        
    }
</style>