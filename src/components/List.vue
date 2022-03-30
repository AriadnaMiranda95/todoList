<template>
  <section>
      <h3>{{name}}</h3>
  <div>
    <task
    :listId="listId"></task>
  </div>
    <input class='add' type="text" placeholder="Añade una tarea" @keypress.enter="add">
  </section>
</template>

<script>
import Task from '@/components/Task'
export default{
  name: 'List',
  components: {Task},
  props: {
    listId: Number,
    name: String
  },
  data () {
    //  const id = parseInt(this.$$attrs)
    return {
    }
  },
  methods: {
    add () {
      console.log(this.$attrs)
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
