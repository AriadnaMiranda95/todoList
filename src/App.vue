<template>
  <div id="app">
    <app-header></app-header>
    <div v-if='mostrar'>
      <modal></modal>
    </div>
    <div v-else>
      <router-view class="container"></router-view>
    </div>
    <app-footer></app-footer>
  </div>
</template>

<script>
import AppHeader from '@/components/AppHeader.vue'
import Modal from '@/components/Modal.vue'
import AppFooter from '@/components/AppFooter'

export default {
  name: 'App',
  components: { AppHeader, AppFooter, Modal },
  data: function () {
    return {
      mostrar: false
    }
  },
  mounted: function comprobarUsuario () {
    const usuario = localStorage.getItem('user')
    if (usuario == null) {
      this.mostrar = true
    } else {
      this.mostrar = false
    }
  }

}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
