<template>
<b-container fluid="sm">
  <b-row class="my-1">
    <b-col sm="2">
      <label for="input-small">E-mail:</label>
    </b-col>
    <b-col sm="10">
      <b-form-input id="input-small" v-model="email" size="sm" placeholder="Enter your email" type=email></b-form-input>
    </b-col>
  </b-row>
  <b-row class="my-1">
    <b-col sm="2">
      <label for="input-small">Password</label>
    </b-col>
    <b-col sm="10">
      <b-form-input id="input-small" v-model="pass" size="sm" placeholder="Enter your password" type=password></b-form-input>
    </b-col>
  </b-row>
  <b-row class="my-1">
    <b-col sm="6" align-v="center">
      <b-button variant="outline-primary"><router-link to="SignUp">Criar Conta</router-link></b-button>
    </b-col>
    <b-col sm="6" align-v="center">
      <b-button variant="outline-primary" v-on:click='this.validateUser'>Entrar</b-button>
    </b-col>
  </b-row>

 <b-row class="my-1">
    <b-col sm="12" align-v="center">
        <b-alert v-model="alert" variant="primary"><a href="#" class="alert-link">{{this.alertText}}</a></b-alert>
    </b-col>
  </b-row>

</b-container>

</template>
<script>
export default {
  created() {
    this.userData = JSON.parse(sessionStorage.getItem('userdata'))
    /*
    sessionStorage.setItem('userdata', JSON.stringify(this.userData))
    sessionStorage.setItem('userdata', JSON.stringify(this.userData))
    console.log(this.userData)
    */
  },
  data: function() {
      return {
          email: '',
          pass: '',
          alert: 'hidden',
          alertText: '',
          userData: {}
      }
  },
  methods: {
      validateUser: function(){
          console.log(this.userData)
        if (this.userData.length > 0) {
            if(this.userData.find(x => x.email === this.email && x.pass === this.pass)){
                this.redirectUser()
            } else {
                this.invalidateUser()
            }
        } else {
            this.invalidateUser()
        }
       // console.log()  
      },
      invalidateUser: function() {
        this.alert = 'show'
        this.alertText = 'Falha no login. Favor criar conta'
      },
      redirectUser: function() {
        this.alert = 'show'
        this.alertText = 'Login realizado com sucesso!! Redirecionando...'
        sessionStorage.setItem('connected', true)
    console.log(sessionStorage.getItem('connected') )
        setTimeout(() => this.$router.push('/List'), 600)
      }
  }
}
</script>