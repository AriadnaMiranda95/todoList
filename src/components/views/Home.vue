<template>
 <div class="container">
    <h3>Tableros de {{userName}}</h3>
    <div class="boards-collection">
      <input type="text" placeholder="Añade un nuevo panel" v-model="boardName" @keyup.enter="add()">
      <board-card v-for="(board, index) in boards"
       :key="index"
       :name="board.name"
       :id="board.id">
       </board-card>
    </div>
  </div>
</template>

<script>
import BoardCard from '@/components/BoardCard'

export default{
  name: 'home-view',
  components: {BoardCard},
  data () {
    console.log(localStorage.user)
    return {
      boardName: '',
      boards: JSON.parse(localStorage.getItem('user')).tableros,
      userName: JSON.parse(localStorage.getItem('user')).name

    }
  },

  methods: {
    add () {
      const user = JSON.parse(localStorage.getItem('user'))
      const tablero = {
        id: user.tableros.length,
        name: this.boardName,
        lists: []
      }
      user.tableros.push(tablero)
      localStorage.setItem('user', JSON.stringify(user))
      this.$router.go(0)
    }
  }
}
</script>

<style scoped>
.container{
  width: 100%;
  height: 120%;
}
  h3{
    text-align: left;
    margin: 1.5rem;
    font-size: 1.8em;
    font-family: 'Oswald', sans-serif;
    font-family: 'Yanone Kaffeesatz', sans-serif;
  }

  .boards-collection{
    display: flex;
    flex-flow: row wrap;
    justify-content: center;
    padding-top: 1rem;
  }

  input{
    box-sizing: border-box;
    background-color: #b68ac4;
    border: 2px solid #b68ac4;
    border-radius: 3px;
    font-size: 1.1rem;
    outline: 0;
    padding: 0.5rem;
    transition: all 600ms ease;
    text-align: center;

  }

  input:focus, input:active{
    background-color: white;
    color: #546E7A;
  }

  input::placeholder{
    color: white;
  }

  board-card{
  display: flex;
  justify-content: space-between;
  }
</style>
