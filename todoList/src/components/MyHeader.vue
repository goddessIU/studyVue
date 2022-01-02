<template>
  <header>
    <input type="text" placeholder="请输入" @keyup.enter="add" v-model="title"/>
  </header>
</template>

<script>
import {nanoid} from 'nanoid';
export default {
  name: "MyHeader",
  data() {
      return {
          title: ''
      }
  },
  methods: {
      add() {
          const value = this.title.trim();
          const todoObj = {id:nanoid(), name:value, done: false};
          this.$emit('addTodo', todoObj);
          this.title = '';
      }
  }
};
</script>

<style scoped> 
</style>