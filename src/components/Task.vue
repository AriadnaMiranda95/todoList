<template>
<div class="">
  <h1>...</h1>
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
