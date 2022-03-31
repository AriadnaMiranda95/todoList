<template lang='html'>
  <section class='container'>
    <h3><span>Mis Paneles</span> ➭ {{name}}</h3>
       <input type="text"
        placeholder="Añadir lista"
        v-model="listName"
        @keyup.enter="add()">
    <div class="list-collection">
      <list v-for="(list, index) in lists"
      :key="index"
      :name="list.name"
      :id="list.id"
      class="list">
      </list>
    </div>
  </section>

</template>

<script>
import List from '@/components/List'

export default {
  name: 'board-view',
  components: {List},
  props: {
    name: String
  },
  data () {
    const id = parseInt(this.$route.params.id)
    return {
      listName: '',
      lists: JSON.parse(localStorage.getItem('user')).tableros[id].lists,
      boardName: JSON.parse(localStorage.getItem('user')).tableros

    }
  },
  methods: {
    add () {
      const user = JSON.parse(localStorage.getItem('user'))
      const id = this.$route.params.id
      const list = {
        id: user.tableros[id].lists.length,
        name: this.listName,
        tasks: []
      }
      user.tableros[id].lists.push(list)
      localStorage.setItem('user', JSON.stringify(user))
      this.$router.go(0)
    }
  }
}
</script>

<style scoped>
  .list-collection{
    margin: 1em 0;
    display: flex;
    flex-flow: row wrap;
    justify-content: flex-start;
    align-items: baseline;
    padding: 1em;

  }

  section{
    text-align: left;
  }

  h3{
    color: #37474f;
    text-align: left;
    margin: 1.5rem;
  }

  input{
    background-color: #b68ac4;
    width: 200px !important;
    height: 50px;
    border: 0;
    border-radius: 3px;
    box-shadow: 0 0 0 0.5px rgba(49,49,93,.03),
      0 2px 5px 0 rgba(49,49,93,.1),
      0 1px 2px 0 rgba(0,0,0,.08);
    color: #607d8b;
    font-size: 1rem;
    text-align: center;
    margin: 0 1.5em ;
    outline: 0;
    transition: all 600ms ease;
  }
  .list:hover{
    background-color: #b979cc;
    color: white;
  }

  input:active, input:focus{
    background-color: #fafafa;
  }

  input::placeholder{
    color: #fafafa;
  }

  span{
    color: #546e7a;
  }
</style>
