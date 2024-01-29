<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <TodoList :propsdata="todoItems" v-on:removeItem="removeOneItem" v-on:toggleItem="toggleOneItem"></TodoList>
    <TodoFooter v-on:clearAll="clearAllItems"></TodoFooter>
  </div>
</template>

<script>
  import TodoHeader from './components/TodoHeader.vue';
  import TodoInput from './components/TodoInput.vue';
  import TodoList from './components/TodoList.vue';
  import TodoFooter from './components/TodoFooter.vue';

  
  export default {
    components: {
      TodoHeader,
      TodoInput,
      TodoList,
      TodoFooter
    },
    methods : {
      removeOneItem(todoItem, index) {
        localStorage.removeItem(todoItem.item);
        this.todoItems.splice(index, 1);
      },
      toggleOneItem(todoItem, index) {
        this.todoItems[index].completed = !this.todoItems[index].completed
        localStorage.removeItem(todoItem);
        localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
      },
      addOneItem(todoItem) {
        console.log(todoItem);
        let obj = {
                    completed : false,
                    item : todoItem
        }
        localStorage.setItem(todoItem, JSON.stringify(obj));
        this.todoItems.push(obj);
      },
      clearAllItems() {
        localStorage.clear();
        this.todoItems = [];
      }
    },
    data() {
      return {
        todoItems : []
      }
    },
    created() {
            console.log('created');
            if(localStorage.length > 0){
                for(let a=0; a<localStorage.length; a++){
                    this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(a))));
                }
            }
        }
  }
</script>

<style>

body {
  text-align: center;
  background-color: #f6f6f6;
}

input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove; 
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}

</style>