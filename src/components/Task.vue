<template>
<button class="task" @click="changeState()">
  {{ name }}
</button>
</template>

<script>
export default {
  name: 'Task',
  props: {
    name: String,
    id: Number
  },
  methods: {
    changeState () {
      // Aqui cambio del localstorage el estado del task
      const idTablero = this.$route.params.id
      const idLista = this.$options.parent.$options.propsData.id
      const idTask = this.id
      const user = JSON.parse(localStorage.getItem('user')).tableros[idTablero].lists[idLista].tasks[idTask]['completed']
      console.log(user)
    }
  }
}
</script>

<style>

</style>
