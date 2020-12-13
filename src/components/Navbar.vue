<script>
    export default {
        name: 'Navbar'
    }
</script>

<template>
<div>
  <b-navbar toggleable="lg" type="dark" variant="info">

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
    <b-navbar-brand @click='redirect("")'>
      <img class="navbar-logo" src="../icons/igti.png"  width="100" height="50" alt="igti">
    </b-navbar-brand>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>    
        <b-nav-item @click='redirect("")'>Home</b-nav-item>
        <b-nav-item @click='redirect("List")'>Products</b-nav-item>
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        <b-nav-form>
            <b-nav-item @click='redirect("SignIn")'>SignIn</b-nav-item>
            <b-nav-item @click='redirect("SignUp")'>SignUp</b-nav-item>
            <b-nav-item @click='logout'>Logout</b-nav-item>
        </b-nav-form>


        
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</div>
</template>

<script>
export default {
  data: function() {
    return {

    }
  },
  methods: {
    logout: function (){
      sessionStorage.setItem('connected', false)
      setTimeout(() => this.$router.push('/SignIn'), 600)
    },
    redirect: function (page) {
      setTimeout(() => this.$router.push(`/${page}`), 100)
    }
  }
}
</script>