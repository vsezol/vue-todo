<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title" />
    <button type="submit">Create</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: ''
    }
  },
  methods: {
    onSubmit() {
      if (this.title.trim()) {
        const humanDate = new Date().toLocaleString('en-Us', {
          hour: 'numeric',
          minute: 'numeric',
          second: 'numeric'
        })
        const newTodo = {
          id: humanDate,
          title: this.title,
          completed: false
        }
        this.title = ''
        this.$emit('add-todo', newTodo)
      }
    }
  }
}
</script>

<style lang="sass">
form
  width: 100%
  margin: 0 auto
  max-width: 720px
  display: flex

input
  flex-grow: 1
  border: 1px solid #ccc
  border-radius: 5px
  padding: 5px
  font-size: 1rem

button
  border-radius: 5px
  padding: 5px
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
