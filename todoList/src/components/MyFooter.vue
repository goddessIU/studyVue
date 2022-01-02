<template>
  <div v-show="total"><input type="checkbox" v-model="isAll">全选 完成<span>{{hasdone}}</span> 全部 <span>{{total}}</span> <button @click="clearAll">清除全部</button></div>
</template>

<script>
export default {
  name: "MyFooter",
  props: ['todos'],
  computed: {
      total() {
          return this.todos.length;
      },
      hasdone() {
          return this.todos.reduce((pre, cur) => pre += (cur.done ? 1 : 0), 0);
      },
      isAll: {
          get() {
              return this.total === this.hasdone;
          },
          set(value) {
              this.$emit('click-all', value);
          }
      }
  },
  methods: {
      clearAll() {
          this.$emit('clear-all');
      }
  }
};
</script>

<style>
</style>