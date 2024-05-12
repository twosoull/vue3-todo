
import TodoList from './components/TodoList.vue';
<template>
  <TodoHeader />
  <TodoInput @add="addTodoItem"/>
  <TodoList :todoItems="todoItems" @remove="removeTodoItem"/>  
</template>

<script>
import { ref } from 'vue';
  import TodoHeader from './components/TodoHeader.vue';
  import TodoInput from './components/TodoInput.vue';
  import TodoList from './components/TodoList.vue';

  export default {
    components :{
      TodoInput,
      TodoHeader,
      TodoList
    },
    setup(){
      const todoItems = ref([]);

      //methods
      //외부에 영향을 주지 않고 독립적인 일을 해야한다. 
      //그러므로 바로 todoItems에 넣지않고 독립적인 array를 반환한다.
      function fetchTodos(){ 
        const result = [];
        for(let i = 0; i < localStorage.length; i++){
           const todoItem = localStorage.key(i);
           result.push(todoItem);
        }
        return result;
      }
      todoItems.value = fetchTodos();

      function addTodoItem(todo){
        todoItems.value.push(todo);
        localStorage.setItem(todo,todo);
      }

      return {todoItems,addTodoItem};
    },
    methods :{
      removeTodoItem(item,index){
        this.todoItems.splice(index,1);
        localStorage.removeItem(item);
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>