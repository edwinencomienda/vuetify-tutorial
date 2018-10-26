<template>
  <div class="">
    <h1>
        <div>ID: {{ todo.id }}</div>
        <div>Title: {{ todo.title }}</div>
        <div>Completed: {{ todo.completed }}</div>
    </h1>
  </div>
</template>

<script>
export default {
  data () {
    return {
      todo: '',
      loading: false
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.loading = true
      const id = this.$route.params.id // this is the router object that will get the params
      axios.get(`https://jsonplaceholder.typicode.com/todos/${id}`).then(response => {
        this.todo = response.data
        this.loading = false
      })
    }
  }
}
</script>
