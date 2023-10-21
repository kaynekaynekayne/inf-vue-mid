<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
        <span class="addContainer" @click="addTodo">
            <i class="fas fa-plus addBtn"></i>
        </span>

        <AlertModal v-if="showModal" @close="showModal = false">
            <h3 slot="header">
                경고!
            </h3>
            <div slot="body">
                입력하세요
            </div>
            <div slot="footer">
                copy right
            </div>
        </AlertModal>
    </div>
</template>

<script>
    import AlertModal from './common/AlertModal.vue';

    export default {
        data(){
            return {
                newTodoItem:"",
                showModal:false
            }
        },
        methods: {
            addTodo: function() {
                if(this.newTodoItem !== ""){
                    this.$emit('addTodoItem', this.newTodoItem)
                    this.clearInput();
                } else {
                    this.showModal=!this.showModal
                }
            },
            clearInput: function() {
                this.newTodoItem=""
            }
        },
        components: {
            AlertModal
        }
    }
</script>

<style scoped>
    input:focus {
        outline: none;
    }
    .inputBox {
        background: white;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }
    .inputBox input {
        border:0;
        border-style: none;
        font-size: 0.9rem;
    }
    .addContainer {
        float: right;
        background: linear-gradient(to right, #6478FB, #8763F8);
        display: block;
        width: 3rem;
        border-radius: 0 5px 5px 0;
        cursor: pointer;
    }
    .addBtn {
        color: white;
        vertical-align: middle;
    }
</style>