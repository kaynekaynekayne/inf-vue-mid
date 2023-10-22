<template>
    <div>
        <transition-group name="list" tag="ul">
            <li v-for="(todoItem,i) in propsdata" :key="i" class="shadow">
                <i class="checkBtn fas fa-check" 
                    :class="{checkBtnCompleted: todoItem.completed}"
                    @click="toggleComplete(todoItem, i)"></i>
                <span :class="{textCompleted: todoItem.completed}">{{todoItem.item}}</span>
                <span class="removeBtn" @click="removeTodo(todoItem, i)">
                    <i class="fas fa-trash-alt"></i>
                </span>
            </li>
        </transition-group>
    </div>
</template>

<script>
    export default {
        props:['propsdata'],
        methods:{
            removeTodo(todoItem, i) {
                this.$emit('removeItem', todoItem, i)
            },
            toggleComplete(todoItem, i) {
                this.$emit('toggleItem', todoItem, i)
            }
        },

    }
</script>

<style scoped>
    ul {
        list-style-type: none;
        padding-left: 0px;
        margin-top: 0;
        text-align: left;
    }
    li {
        display: flex;
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin: 0.5rem 0;
        padding: 0 0.9rem;
        background: white;
        border-radius: 5px;
    }
    .checkBtn {
        line-height: 45px;
        color: #62acde;
        margin-right: 5px;
        cursor:pointer;
    }
    .checkBtnCompleted {
        color: #b3adad;
    }
    .textCompleted {
        text-decoration: line-through;
        color: #b3adad;
    }
    .removeBtn {
        margin-left: auto;
        color: #de4343;
        cursor:pointer;
    }

    .list-enter-active,
    .list-leave-active {
        transition: all 1s;
    }
    .list-enter,
    .list-leave-to {
        opacity: 0;
        transform: translateY(30px);
    }
</style>