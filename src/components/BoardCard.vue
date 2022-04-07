<template>
  <div class="board-card">
    <button class="deleteBoard" @click="deleteBoard()"> X </button>
    <router-link class="board-redirect"
    :to="{name: 'board', params: {name, id}}">
    <span class="board-card-title">{{name}}</span>
    </router-link>
  </div>
</template>

<script>

export default {
  name: 'BoardCard',
  props: {
    id: Number,
    name: String
  },
  data () {
    const idBoard = this.id
    const user = JSON.parse(localStorage.getItem('user'))
    return {
      idBoard,
      show: true,
      user
    }
  },
  methods: {
    deleteBoard () {
      console.log(this.show)
      this.show = !this.show
      this.user.tableros[this.id]['show'] = this.show
      localStorage.setItem('user', JSON.stringify(this.user))
      this.$router.go(0)
    }
  }
}
</script>

<style scoped>

  .board-card {
    /* background-color: rgb(40, 214, 182);
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
    height: 90px; */
    background-color: rgb(40, 214, 182);
    transition: all .5s ease;
    margin: 1em;
    border-radius: 5px;
    width:20%;
    display: flex;
    flex-flow: column nowrap;
    padding: 1em ;
     box-shadow: 5px 5px 24px 5px rgba(0,0,0,0.20);

  }

  .board-redirect{
    text-decoration: none;
  }

  .board-card:hover{
    background-color: #b68ac4;
  }

  .board-card-title{
    font-size: 1.8em;
    font-family: 'Oswald', sans-serif;
    font-family: 'Yanone Kaffeesatz', sans-serif;
    color: white;
    margin: .5em;

  }

  .deleteBoard{
    background-color: transparent;
    border: none;
    font-size: 15px;
    align-self: flex-end;
  }

  .deleteBoard:hover{
    color: white;
    transition: all .25s ease;
    cursor: pointer;
  }

  @media screen and (min-width: 600px) {
    .board-card{
       margin: 1em .5 0 2.6em;
    }
  }
  /*
  @media screen and (min-width: 1024px) {
    .board-card{
      width: 90%;
    }
  } */

</style>
