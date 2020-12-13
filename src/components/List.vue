<template>
  <div v-show="connected === 'true'">
    <b-table striped hover :items="items"></b-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [],
      connected: false
    }
  },
  created() {
     this.connected = sessionStorage.getItem('connected') || 'false'
     
      if(this.connected === 'false'){
        console.log('here')
          setTimeout(() => this.$router.push('/SignIn'), 600)
      } else {
        this.items = JSON.parse(sessionStorage.getItem('userdata'))
        this.items = this.items.map(x => { return { name: x.name, email: x.email }})
      }
  }
}
</script>