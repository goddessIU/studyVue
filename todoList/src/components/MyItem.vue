<template>
  <li><input type="checkbox" :checked="todo.done" @click="store"/><span>{{todo.name}}</span> 
  <button @click="deleteItem(todo.id)">删除</button></li>
</template>

<script>
export default {
  name: "MyItem",
  props: ['todo','storeChecked','deleteTodo'],
  methods: {
    store() {
        this.storeChecked(this.todo.id);
    },
    deleteItem(id) {
        this.deleteTodo(id);
    }
  }
};
</script>

<style>
</style>