<template>
    <button @click="onClick" :style="{background: color}" class="btn">{{text}} </button>
</template>

<script>
export default {
    name: 'Button',
    props: {
        text: String,
        color: String,
    },
    methods: {
        onClick(){
            this.$emit('btn-click')
        }
    }
}
</script>

<style scoped>
    .btn {
        padding: 8px;
        padding-left: 16px;
        padding-right: 16px;
        border: none;
        border-radius: 4px;
        background-color: skyblue;
        color: white;
    }
</style>