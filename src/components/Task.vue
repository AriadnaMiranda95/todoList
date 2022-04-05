<template>
  <div class="task ejemplo" >
    <p @click="changeState()" v-bind:class="isActive" >{{ name }} </p>
    <!-- <p class="time">{{this.actualDate}}</p> -->
    <section class="buttons">
    <button class="delete" @click="deleteTask()"><i class="fa-solid fa-trash-can"></i></button>
    <!-- <button class="showMore" @click="boton()"> <i class="fa-solid fa-circle-info"></i> </button> -->
    <i class="fa-solid fa-circle-info info">
          <p class="time">Fecha creación: <span>{{this.actualDate}}</span></p>
    </i>
    <!-- <ul v-show="mostrar">
            <li class="time">Fecha creación: {{this.actualDate}}</li>
    </ul> -->
    </section>
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
    const actualDate = user.tableros[idTablero].lists[idLista].tasks[idTask]['startDate']
    const endDate = user.tableros[idTablero].lists[idLista].tasks[idTask]['endDate']
    const isActive = completed ? 'inactive' : 'active'
    return {
      completed,
      isActive,
      idLista,
      idTablero,
      idTask,
      user,
      task,
      show: true,
      actualDate,
      endDate
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
    width: 30px;
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

  .time{
    font-size: 11px;
    list-style: none;
    padding:  0 !important;
  }

  .showMore{
    border: none;
    background: none;
    font-size: 1.3em;
  }

  .info{
    color: #47A8BD;
    position: relative;
    font-size: 25px;
    margin: 0 0 0 .2em;
  }

  .info:hover p {
    display: flex;
  }

  .info:hover{
    font-size: 27px;
    color: #3d8fa1;
    transition: all .25s ease;
    cursor: pointer;
  }

  .info p{
    position: absolute;
    width: 150px;
    background-color: #f3d8fc;
    padding: 1em 1.2em !important;
    border-radius: .2em;
    display: flex;
    flex-flow: column nowrap;
    display: none;
    font-family: 'Courier New', Courier, monospace;
    color: black;
    top: 14px;
    left: 30px;
    font-size: 10px;
  }

  .info p span{
    margin: .5em 0;
  }

  .buttons{
    display: flex;
    align-items: center;
  }
  ul{
    padding: 0;
  }

</style>
