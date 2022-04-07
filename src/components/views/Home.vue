<template>
 <div class="container">
    <section>
      <div class="info-content">
    <h3>Tableros de {{userName}}</h3>
     <iframe src="https://www.zeitverschiebung.net/clock-widget-iframe-v2?language=es&size=small&timezone=Atlantic%2FCanary"  frameborder="0" seamless></iframe>     </div>
      <input type="text" placeholder="Añade un nuevo panel" v-model="boardName" @keyup.enter="add()">
    </section>
    <div class="boards-collection">
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
  props: {
    name: String,
    id: Number
  },
  data () {
    const user = JSON.parse(localStorage.getItem('user'))
    const boards = (user.tableros).filter(function (board) {
      return board.show
    })
    // JSON.parse(localStorage.getItem('user')).tableros
    return {
      boardName: '',
      boards: boards,
      userName: JSON.parse(localStorage.getItem('user')).name

    }
  },

  methods: {
    add () {
      const user = JSON.parse(localStorage.getItem('user'))
      const tablero = {
        id: user.tableros.length,
        name: this.boardName,
        show: true,
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
  display: flex;
  flex-flow: column nowrap;
  align-content: center;
}

.container section {
  display: flex;
  justify-content: center;
  flex-flow: column nowrap;
}

.info-content{
  display: flex;
  flex-flow: row wrap;
  width: 100%;
  justify-content: space-around;
}

iframe{
  flex:1 1 300px;
  max-width: 300px;
}

.container section input{
    align-self:  center;
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
  h3{
    text-align: left;
    margin: 1.5rem;
    font-size: 1.8em;
    flex: 1 1 300px;

  }
  .boards-collection{
    display: flex;
    flex-flow: row wrap;
    justify-content: center;
    justify-items: center;
    margin: 2em;
    flex: 4;
  }

  .container section input:focus, .container section input:active{
    background-color: white;
    color: #546E7A;
  }

  input::placeholder{
    color: white;
  }

</style>
