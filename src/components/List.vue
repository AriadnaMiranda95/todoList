<template>
  <section>
      <h3>{{name}}</h3>
  <div>
    <input type="text"
        placeholder="Añadir una tarea a la lista"
        v-model="taskName"
        @keyup.enter="add()">
    <task v-for="(task, index) in tasks"
    :key="index"
    :id="task.id"
    :name="task.name"
    class="task"></task>
  </div>
  </section>
</template>

<script>
import Task from '@/components/Task'
export default{
  name: 'List',
  components: {Task},
  props: {
    name: String,
    id: Number,
    show: Boolean
  },
  data () {
    const user = JSON.parse(localStorage.getItem('user'))
    const idTablero = this.$route.params.id
    const idList = this.id
    const tasks = (user.tableros[idTablero].lists[idList].tasks).filter(function (task) {
      return task.show
    })
    return {
      taskName: '',
      tasks: tasks// user.tableros[idTablero].lists[idList].tasks
    }
  },
  methods: {
    add () {
      const user = JSON.parse(localStorage.getItem('user'))
      const idTablero = this.$route.params.id
      const idList = this.id
      const idTask = user.tableros[idTablero].lists[idList].tasks.length
      const actualDate = Date.now('yyyy-mm-dd')
      const task = {
        id: idTask,
        name: this.taskName,
        startDate: actualDate,
        duration: '',
        endDate: '',
        completed: false,
        show: true
      }
      console.log(task)
      user.tableros[idTablero].lists[idList].tasks.push(task)
      localStorage.setItem('user', JSON.stringify(user))
      this.$router.go(0)
    }
  }
}
</script>
<style scoped>
  section {
    background-color: rgb(237, 224, 243);
    width: 320px !important;
    border-radius: .2em;
    text-align: initial;
    padding: .5em;
     box-shadow: 0 0 0 0.5px rgba(49,49,93,.03),
      0 2px 5px 0 rgba(49,49,93,.1),
      0 1px 2px 0 rgba(0,0,0,.08);
  }
    input{
      width: 99%;
      border: white;
      border-radius: .2em;
      padding: .5em 0;
      margin: .2em 0;
    }

    input::placeholder{
      color: gray;
      padding: 0 .4em;
    }

  .task {
    background-color: white;
    width: 93% !important;
    border-color: white;
    border-radius: .4em;
    padding: .5em 0 .5em .5em;
    margin: .2em 0;
    color: black;

  }

  @media screen and (min-width: 400px) {
      section{
        width: calc(70% - 2rem - 2px);
      }
    }
  @media screen and (min-width: 1024px) {
      section{
        width: calc(33% - 2rem - 2px);
      }
    }
  @media screen and (min-width: 1200px) {
      section{
         width: calc(25% - 2rem - 2px);
      }
    }

</style>
