<template>
  <div class="task ejemplo" >
    <p @click="changeState()" v-bind:class="isActive" >{{ name }} </p>
    <section class="buttons">
    <button class="delete" @click="deleteTask()"><i class="fa-solid fa-trash-can"></i></button>
    <i class="fa-solid fa-circle-info info">
      <div>
          <p class="created_at">Fecha creación: <span>{{this.actualDate}}</span></p>
          <p class="ended_at">Fecha finalizacion: <span>{{this.endDate}}</span></p>
      </div>
    </i>
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
      const moment = require('moment')
      const datenow = moment(new Date()).local().format('DD/MM/YYYY h:mm a')
      this.completed = !this.completed
      this.user.tableros[this.idTablero].lists[this.idLista].tasks[this.idTask]['completed'] = this.completed// !completed
      this.user.tableros[this.idTablero].lists[this.idLista].tasks[this.idTask]['endDate'] = datenow
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

  .task p:hover{
    cursor: pointer;
  }

  .delete{
    width: 30px;
    background-color: transparent;
    font-size: 1.5em;
    border-radius: .2em;
    border: none;
  }

  .delete:hover{
    transform: scale(1.1);
    transition: all .25s ease;cursor: pointer;
  }

  .fa-solid{
    color: #f9617d;
    padding: .2em;
  }

  .fa-solid:hover{
    color: #f04262;
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

  .info:hover div {
    display: flex;
  }

  .info:hover{
    transform: scale(1.1);
    color: #3d8fa1;
    transition: all .2s ease ;
    cursor: pointer;
  }

  .info div{
    display: flex;
    position: absolute;
    flex-flow: column nowrap;
    top: 10px;
    right: 35px;
    display: none;
    background-color: #f3d8fc;
    box-shadow: 6px 8px 13px 1px rgba(0,0,0,0.36);
    border-radius: .2em;
    padding: .2em;
    width: 215px;
  }

  .info p{
    font-family: 'Oswald', sans-serif;
    font-family: 'Yanone Kaffeesatz', sans-serif;
    color: black;
    font-size: 14px;
    letter-spacing: .05em;
    margin:.2em ;
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

  @media screen and (min-width: 500px) {
      .info div {
        right: 0;
        left: 35px;
        overflow: hidden;
      }

    }

</style>
