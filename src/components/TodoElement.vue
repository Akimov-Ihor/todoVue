<template>
  <li>
    <span v-bind:class="{done:todo.completed}">
      <input type="checkbox" v-on:change="todo.completed=!todo.completed" />
      <span>{{index+1}}</span>
      {{todo.title}}
    </span>
    <button class="rmv" v-on:click="$emit('remove-todo',todo.id)">
        &times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index:Number
  }
}

</script>

<style  scoped>
li {
  border: 2px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: 0.5em 3em;
  margin-top: 1em;
}
input {
  margin-right: 1rem;
}
.rmv {
  background: black;
  color: #fff;
  border-radius: 50%;
  font-weight: bold;
  outline: none;
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
</style>