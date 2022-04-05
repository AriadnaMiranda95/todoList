<template>
  <div class="task ejemplo" >
    <p @click="changeState()" v-bind:class="isActive" >{{ name }} </p>
    <button class="delete" @click="deleteTask()"><i class="fa-solid fa-trash-can"></i></button>
  </div>
</template>

<script>
export default {
  name: 'Task',
  props: {
    name: String,
    id: Number
  },
  data () {
    const idTablero = this.$route.params.id
    const idLista = this.$options.parent.$options.propsData.id
    const idTask = this.id
    const user = JSON.parse(localStorage.getItem('user'))
    const completed = user.tableros[idTablero].lists[idLista].tasks[idTask]['completed']
    const task = user.tableros[idTablero].lists[idLista].tasks[idTask]
    const isActive = completed ? 'inactive' : 'active'
    return {
      completed,
      isActive,
      idLista,
      idTablero,
      idTask,
      user,
      task,
      show: true
    }
  },
  methods: {
    changeState () {
      this.completed = !this.completed
      this.user.tableros[this.idTablero].lists[this.idLista].tasks[this.idTask]['completed'] = this.completed// !completed
      localStorage.setItem('user', JSON.stringify(this.user))
      console.log(this.show)
      this.$router.go(0)
    },
    deleteTask () {
      this.show = false
      this.user.tableros[this.idTablero].lists[this.idLista].tasks[this.idTask]['show'] = this.show
      localStorage.setItem('user', JSON.stringify(this.user))
      this.$router.go(0)
    }
  }
}
</script>

<style>
  .inactive{
    text-decoration: line-through;
  }

  .active{
    text-decoration: none;

  }
  .task{
    display: flex;
    justify-content: space-between;
    padding: .5em !important;
  }

.task:hover{
  font-weight: bolder;
}

  .delete{
    width: 50px;
    background-color: transparent;
    font-size: 1.5em;
    border-radius: .2em;
    border: none;
  }

  .delete:hover{
    font-size: 1.8em;
    transition: all .25s ease;cursor: pointer;
  }

  .fa-solid{
    color: #f9617d;
    padding: .2em;
  }

  .fa-solid:hover{
    color: #f04262;

  }

</style>
