<template>
  <li>
    <span v-bind:class="{ done: todo.completed }">
      <input type="checkbox" v-on:change="todo.completed = !todo.completed" />
      <strong>{{ index + 1 }}</strong>
      {{ todo.title | uppercase }}
    </span>
    <button class="rm-btn" v-on:click="$emit('remove-todo', todo.id)">
      &times;
    </button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  filters: {
    uppercase(value) {
      return value.toUpperCase()
    }
  }
}
</script>

<style lang="sass">
li
  border: 1px solid #ccc
  border-radius: 5px
  display: flex
  justify-content: space-between
  padding: 10px 20px
  margin-bottom: 1rem

input
  margin-right: 1rem

.done
  text-decoration: line-through

.rm-btn
  border-radius: 5px
  border: none
  font-size: 1rem
  color: black
  cursor: pointer
  background: #ccc
  outline: none
  &:hover
    background: black
    color: white
</style>
