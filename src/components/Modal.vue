<template>
  <div id="modal-container">
    <form id="modal-form" action="/">
      <h1>Bienvenido a VueTrello</h1>
      <p>¿Con qué nombre quieres que te llame?</p>
      <input type="text" :name="name" class="name">
      <section class="botones">
        <input type="submit" value="Enviar" class="enviar" @click="crearUsuario()">
      </section>
    </form>
  </div>
</template>

<script>
export default {
  name: 'modal',
  props: {
    id: Number,
    name: String
  },
  methods: {
    crearUsuario () {
      const userName = document.querySelector('.name')
      const datosUsuario = {
        name: userName.value,
        tableros: []
      }
      localStorage.setItem('user', JSON.stringify(datosUsuario))
    }
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Oswald&family=Yanone+Kaffeesatz&display=swap');
  #modal-container{
    width: 100%;
    height: 600px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  #modal-form{
    background-color: rgb(231, 129, 223);
    width: 60%;
    height: 40%;
    display: flex;
    flex-flow: column nowrap;
    justify-content: center;
    align-items: center;
    border-radius: .7em;
  }
  h1{
    font-family: 'Yanone Kaffeesatz', sans-serif;
    font-family: 'Oswald', sans-serif;
    background-color: white;
    color: rgb(88, 92, 92);
    width: 98%;
    border-radius: .1em;
    text-align: center;
  }

  p{

    font-family: 'Yanone Kaffeesatz', sans-serif;
    font-size: 1.4em;
    color: white;
    margin: 0 !important;
  }

  span{
    color: rgb(247, 247, 247);
    font-size: 30px;
  }
  .name{
    width: 50%;
    margin: 1em 0 .7em 0;
    border: white;
    border-radius: .5em;
    padding: .5em;
  }

  .enviar, .cancelar{
    border-radius: .5em;
    padding: .7em ;
    background-color: white;
    border: white;
    margin: .5em;
    font-family: 'Oswald', sans-serif;
    font-family: 'Yanone Kaffeesatz', sans-serif;
    font-size: 1.1em;
  }

  .enviar:hover, .cancelar:hover{
    color: white;
    background-color:rgb(139, 27, 134);
  }
</style>
