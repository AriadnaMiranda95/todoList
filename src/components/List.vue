<template>
  <section>
      <h3>{{name}}</h3>
  <div>
    <input type="text"
        placeholder="Añadir lista"
        v-model="taskName"
        @keyup.enter="add()">
    <task v-for="(task, index) in tasks"
    :key="index"
    :id="task.id"
    :name="task.name"></task>
  </div>
  </section>
</template>

<script>
import Task from '@/components/Task'
export default{
  name: 'List',
  components: {Task},
  props: {
    name: String
  },
  data () {
    const user = JSON.parse(localStorage.getItem('user'))
    const idTablero = this.$route.params.id
    const idList = this.$attrs.id
    return {
      taskName: '',
      tasks: user.tableros[idTablero].lists[idList].tasks
    }
  },
  methods: {
    add () {
      const user = JSON.parse(localStorage.getItem('user'))
      const idTablero = this.$route.params.id
      const idList = this.$attrs.id
      const idTask = user.tableros[idTablero].lists[idList].tasks.length
      const actualDate = Date.now()
      const task = {
        id: idTask,
        name: this.taskName,
        startDate: actualDate,
        duration: '',
        endDate: ''
      }
      console.log(task)
      user.tableros[idTablero].lists[idList].tasks.push(task)
      localStorage.setItem('user', JSON.stringify(user))
      //  this.$router.go(0)
    }
  }
}
</script>
<style scoped>
  section {
    background-color: rgb(237, 224, 243);
    margin: .5em;
    width: 300px !important;
    border-radius: .2em;
    text-align: initial;
    padding: .5em;
     box-shadow: 0 0 0 0.5px rgba(49,49,93,.03),
      0 2px 5px 0 rgba(49,49,93,.1),
      0 1px 2px 0 rgba(0,0,0,.08);
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
