<template>
    <div class="clearAllContainer">
        <span @click="clearTodo" class="clearAllBtn">Clear All</span>
    </div>
</template>

<script>
    export default {
        methods: {
            clearTodo() {
                this.$emit('clearAll');
            }
        }
    }
</script>

<style scoped>
    .clearAllContainer {
        width: 8.5rem;
        height: 50px;
        line-height: 50px;
        background-color: white;
        border-radius: 5px;
        margin: 0 auto;
        cursor: pointer;
    }
    .clearAllBtn {
        color: #e20303;
        /* 추가 */
        display: block;
    }
</style>
