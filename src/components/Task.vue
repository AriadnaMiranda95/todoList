<template>
<section class="task">
  <h1>{{ name }}</h1>
</section>
</template>

<script>
export default {
  name: 'Task',
  props: {
    name: String,
    id: Number
  }
}
</script>

<style>

.task {
    background-color: rgb(237, 224, 243);
    margin: .5em;
    width: 100px !important;
    border-radius: .2em;
    text-align: initial;
    padding: .5em;
     box-shadow: 0 0 0 0.5px rgba(49,49,93,.03),
      0 2px 5px 0 rgba(49,49,93,.1),
      0 1px 2px 0 rgba(0,0,0,.08);
  }

</style>
