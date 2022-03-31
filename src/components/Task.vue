<template>
<button class="task">
  {{ name }}
</button>
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

</style>
