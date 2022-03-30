<template>
  <router-link
  class="board-card"
  :to="{name: 'board', params: {name, id}}">
  <span class="board-card-title">{{name}}</span>
  </router-link>
</template>

<script>

export default {
  name: 'BoardCard',
  props: {
    id: Number,
    name: String
  }
}
</script>

<style scoped>

  .board-card {
    background-color: rgb(40, 214, 182);
    box-shadow: 0 0 0 0.5px rgba(49,49,93,.03),
    0 2px 5px 0 rgba(49,49,93,.1),
    0 1px 2px 0 rgba(0,0,0,.08);
    box-sizing: border-box;
    border-radius: 5px;
    color: #fafafa;
    margin: 0.5rem 1.5rem;
    padding: 1rem;
    text-align: left;
    text-decoration: none;
    transition: all 600ms ease;
    width: 90%;
    height: 90px;
  }

  .board-card:hover{
    background-color: #b68ac4;
    font-size: 2em;
    font-weight: bold;
  }
  .board-card-title{
    font-size: 25px;
    font-family: 'Oswald', sans-serif;
    font-family: 'Yanone Kaffeesatz', sans-serif;

  }

  @media screen and (min-width: 600px) {
    .board-card{
      width: 80%;
    }
  }
  @media screen and (min-width: 1024px) {
    .board-card{
      width: 90%;
    }
  }

</style>
