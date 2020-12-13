<template>
  <div id="app">
    <div id="navbar">
      <Navbar />
    </div>
    <router-view/>
  </div>
</template>

<script>
import Navbar from './components/Navbar'
export default {
  name: 'App',
  components: {
    Navbar
  },
  beforeCreate: function() {
    this.$userData = [...this.$userData, {email: 'teste@teste.com', pass: '111'}]
    //console.log('oi')
    //console.log(this.$userData)
  },
  methods: {
    teste: function() {
      console.log("teste aqui")
    }
  }
}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
