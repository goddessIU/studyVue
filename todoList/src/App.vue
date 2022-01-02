<template>
  <div id="rooter">
    <MyHeader @addTodo="addTodo" />
    <MyList :todos="todos" :storeChecked="storeChecked" 
    :deleteTodo="deleteTodo"/>
    <MyFooter :todos="todos"  @clear-all="clearAll" @click-all="clickAll"/>
  </div>
</template>

<script>
import MyHeader from "./components/MyHeader.vue";
import MyList from "./components/MyList.vue";
import MyFooter from "./components/MyFooter.vue";
export default {
  name: "App",
  components: {
    MyHeader,
    MyList,
    MyFooter,
  },
  data() {
    return { todos: JSON.parse(localStorage.getItem('todos') )|| [] };
  },
  methods: {
    addTodo(todoObj) {
      this.todos.unshift(todoObj);
    },
    storeChecked(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) {
          todo.done = !todo.done;
        }
      })
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    clearAll() {
      this.todos = this.todos.filter((todo) => todo.done === false);
    },
    clickAll(value) {
      this.todos.forEach((todo) => todo.done = value);
    } 
  },
  watch: {
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem('todos', JSON.stringify(value));
      }
    }
  }
};
</script>

<style>
</style>