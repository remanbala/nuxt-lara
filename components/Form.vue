<template>
  <div class="container">
    <div v-for="(todo,index) in todos"
      :key="index"
      class="bg-light mt-5 mb-5"
      style="padding: 20px"
    >
      {{ todo.todoItem }} 
    </div>
{{todos}}
    

    <h1 class="pt-5 text-center">Form</h1>

    <form @submit.prevent="addTodo">
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">Add Todo Item</label>
        <input
          type="text"
          class="form-control"
          name="todoItem"
          v-model="todoItem"
          id="todoItem"
          required
        />
      </div>
      <button type="submit" class="btn btn-primary">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  async asyncData({$axios}) {
  //let {todo}= await $axios.$get('/todo')
  let data = (await $axios.get('/todo')).data
  return {
    todos: data
  }
 
  },
 
  data() {
    return {
      todoItem: '',
      todos: []
    }
  },
  methods: {
    async addTodo() {
      await this.$axios.$post('/todo', {
        todoItem: this.todoItem,
      })
    },
  },
}
</script>
