<template>
  <div id="app">
    <todo-header></todo-header>
    <todo-input @add="addOneItem"></todo-input>
    <todo-list v-bind:propsdata="todoItems" @toggle="toggleOneItem" 
    @remove="removeOneItem"></todo-list>
    <todo-footer @clear="clearAllItem"></todo-footer>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {
  data: function(){
    return{
      todoItems: []
    }
  },
  methods: {
    addOneItem: function(newTodoItem){
      var obj = {completed: false, item: newTodoItem};
      localStorage.setItem(newTodoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    toggleOneItem: function(todoItem, index){
      this.todoItems[index].completed = !this.todoItems[index].completed;
      localStorage.removeItem(this.todoItems[index].item);
      localStorage.setItem(this.todoItems[index].item, JSON.stringify(this.todoItems[index]));
    },
    removeOneItem: function(todoItem, index){
      localStorage.removeItem(this.todoItems[index].item);
      this.todoItems.splice(index, 1);
    },
    clearAllItem: function(){
      localStorage.clear();
      this.todoItems = [];
    }
  },
  created: function(){
    if(localStorage.length > 0){
      for(var i = 0; i < localStorage.length; i++){
        if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        }
      }
    }
  },
  components: {
    'todo-header': TodoHeader,
    'todo-input': TodoInput,
    'todo-list': TodoList,
    'todo-footer': TodoFooter,
  }
}
</script>

<style>
body{
  text-align: center;
  background-color: #F6F6F6;
}

input{
  border-style: groove;
  width: 200px;
}

button{
  border-style: groove;
}

.shadow{
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
