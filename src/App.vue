<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput @addTodoItem="addOneItem"></TodoInput>
    <TodoList 
      :propsdata="todoItems" 
      @removeItem="removeOneItem"
      @toggleItem="toggleOneItem"  
    ></TodoList>
    <TodoFooter
      @clearAll="clearAllItems"
    ></TodoFooter>
  </div>
</template>

<script>
  import TodoHeader from './components/TodoHeader.vue'
  import TodoInput from './components/TodoInput.vue'
  import TodoList from './components/TodoList.vue'
  import TodoFooter from './components/TodoFooter.vue'

  export default {
    data(){
      return {
        todoItems:[]
      }
    },
    methods: {
      //실질적인 데이터처리는 전부 App.vue에서 함
      addOneItem(todoItem) {
        const obj={completed: false, item:todoItem};
        localStorage.setItem(todoItem, JSON.stringify(obj));
        this.todoItems.push(obj);
      },
      removeOneItem(todoItem, i){
        localStorage.removeItem(todoItem.item);
        this.todoItems.splice(i, 1); //기존 배열 건드림
        
        //filter는 새로운 배열을 반환하기 때문에
        //splice처럼 화면에 바로 반영하고 싶은 경우 밑처럼 써야함
        // this.todoItems=this.todoItems.filter(item=>item!==todoItem);
      },
      toggleOneItem(todoItem,i){
        this.todoItems[i].completed=!this.todoItems[i].completed;
        localStorage.removeItem(todoItem.item);
        localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
      },
      clearAllItems(){
        localStorage.clear();
        this.todoItems=[];
      }
    },
    created: function() {
        //인스턴스가 생성되는 시점에 로직 호출
        if (localStorage.length > 0) {
            for (let i=0; i<localStorage.length; i++) {
                if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
                    // console.log(JSON.parse(localStorage.getItem(localStorage.key(i))));
                    this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))))
                }
            }
        }
    },
    components: {
      TodoHeader,
      TodoInput,
      TodoList,
      TodoFooter
    },
  }
</script>

<style>
body {
  font-family: 'Ubuntu', sans-serif;
  text-align: center;
  background-color: #F6F6F6;
}

input {
  border-style:groove;
  width: 200px;
}

button {
  border-style: groove;
}

.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
