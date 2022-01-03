<template>
  <li><input type="checkbox"  :checked="todo.done" @click="store"/><span v-show="!todo.isEdit">{{todo.name}}</span>
  <input 
  type="text"
  :value="todo.name"
  ref="inputTitle"
  v-show="todo.isEdit"
  @blur="handleBlur(todo, $event)"
  > 
  <button @click="deleteItem(todo.id)">删除</button><button @click="handleClick(todo)">修改</button></li>
  
</template>

<script>
import pubusb from 'pubsub-js';
export default {
  name: "MyItem",
  props: ['todo'],
  methods: {
    store() {
        this.$bus.$emit('storeChecked', this.todo.id);
    },
    deleteItem(id) {
        pubusb.publish('deleteTodo', id);
    },
    handleClick(todo) {
      if (Object.prototype.hasOwnProperty.call(todo, 'isEdit')) {
        todo.isEdit = true;
      } else {
        this.$set(todo, 'isEdit', true);
      }
      this.$nextTick(function() {
        this.$refs.inputTitle.focus();
      }) 
    },
    handleBlur(todo, e) {
      todo.isEdit = false;
      if (e.target.value.trim() === '') alert('false');
      this.$bus.$emit('handleBlur', todo.id, e.target.value);
    }
  }
};
</script>

<style>
</style>