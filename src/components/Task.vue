<template>
<div class="">
  <h1>...</h1>
  <input class='add' type="text" placeholder="Añade una tarea" v-model="title" @keypress.enter="add">
</div>
</template>

<script>
export default {
  name: 'Task',
  listId: '',
  props: {
    name: String,
    listId: Number
  },
  data () {
    return {
      title: ''
    }
  },
  methods: {
    add () {
      console.log(this.listId)
    }
  }
}
</script>

<style>

.add{
    box-sizing: border-box;
    border-radius: 3px;
    border-color: rgb(255, 255, 255);
    padding: 0.5rem;
    transition: all 600ms ease;
    text-align: center;
    width: 100%;
}

</style>
