<template>
  <ul>
    <MyItem 
    v-for="todo in todos"
    v-bind:key="todo.id"
    :todo="todo"
    />
  </ul>
</template>

<script>
import MyItem from "./MyItem.vue";
export default {
  name: "MyList",
  components: { MyItem },
  props: ["todos"],
};
</script>

<style>
</style>