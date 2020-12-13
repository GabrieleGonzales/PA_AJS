<template>
<b-container fluid="sm">
  <b-row class="my-1">
    <b-col sm="2">
      <label for="input-small">Name:</label>
    </b-col>
    <b-col sm="10">
      <b-form-input id="input-small" v-model="name" size="sm" placeholder="Enter your name" type=text :state='(this.errors.find(x => x.field === "name")).valid'></b-form-input>
      <b-form-invalid-feedback id="input-live-feedback">
        {{ (this.errors.find(x => x.field === "name")).err }}
      </b-form-invalid-feedback>
    </b-col>
  </b-row>
  <b-row class="my-1">
    <b-col sm="2">
      <label for="input-small">E-mail:</label>
    </b-col>
    <b-col sm="10">
      <b-form-input id="input-small" v-model="email" size="sm" placeholder="Enter your e-mail" type=email :state='(this.errors.find(x => x.field === "email")).valid'></b-form-input>
      <b-form-invalid-feedback id="input-live-feedback">
        {{ (this.errors.find(x => x.field === "email")).err }}
      </b-form-invalid-feedback>
    </b-col>
  </b-row>
  
  <b-row class="my-1">
    <b-col sm="2">
      <label for="input-small">Confirm e-mail:</label>
    </b-col>
    <b-col sm="10">
      <b-form-input id="input-small" v-model="emailConfirm" size="sm" placeholder="Enter your email" type=email :state='(this.errors.find(x => x.field === "emailConfirm")).valid'></b-form-input>
      <b-form-invalid-feedback id="input-live-feedback">
        {{ (this.errors.find(x => x.field === "emailConfirm")).err }}
      </b-form-invalid-feedback>
    </b-col>
  </b-row>
  <b-row class="my-1">
    <b-col sm="2">
      <label for="input-small">Password</label>
    </b-col>
    <b-col sm="10">
      <b-form-input id="input-small" v-model="pass" size="sm" placeholder="Enter your password" type=password :state='(this.errors.find(x => x.field === "pass")).valid'></b-form-input>
      <b-form-invalid-feedback id="input-live-feedback">
        {{ (this.errors.find(x => x.field === "pass")).err }}
      </b-form-invalid-feedback>
    </b-col>
  </b-row>
  <b-row class="my-1">
    <b-col sm="2">
      <label for="input-small">Confirm Password</label>
    </b-col>
    <b-col sm="10">
      <b-form-input id="input-small" v-model="passConfirm" size="sm" placeholder="Enter your password" type=password :state='(this.errors.find(x => x.field === "passConfirm")).valid'></b-form-input>
      <b-form-invalid-feedback id="input-live-feedback">
        {{ (this.errors.find(x => x.field === "passConfirm")).err }}
      </b-form-invalid-feedback>
    </b-col>
  </b-row>
  <b-row class="my-1">
    <b-col sm="6" align-v="center">
    </b-col>
    <b-col sm="6" align-v="center">
      <b-button variant="outline-primary" :disabled='this.submitEnable' v-on:click='this.validateUser'>Submit</b-button>
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
  data: function() {
      return {
          name: '',
          email: '',
          emailConfirm: '',
          pass: '',
          passConfirm: '',
          alert: 'hidden',
          alertText: '',
          userData: {},
          errors: [{}],
          error: 0,
          submitEnable: 'disabled'
      }
  },
  created () {
    // sessionStorage.setItem('connected', false)
    this.userData = JSON.parse(sessionStorage.getItem('userdata'))
    
    this.errors = [
      {
        field: 'name',
        err: '',
        regex: '^[a-zA-Z\\s]*$',
        valid: false
      },
      {
        field: 'email',
        err: '',
        regex: '[a-zA-Z0-9]+@[a-zA-Z]+(\.[a-zA-Z]+){1,2}$',
        valid: false
      },
      {
        field: 'emailConfirm',
        err: '',
        valid: false
      },
      {
        field: 'pass',
        err: '',
        regex: '^.{6,}$',
        valid: false
      },
      {
        field: 'passConfirm',
        err: '',
        valid: false
      },
    ]
  },
  watch: {
    name: function() {
      let regex_name = this.errors.find(x => x.field === "name")
      if(this.name.match(regex_name.regex) === null) {
        regex_name.err = 'Favor inserir apenas caracteres de texto e espaços'
        regex_name.valid = false
        this.errors = this.errors.filter(x => x.field !== "name")
        this.errors = [...this.errors, regex_name]
      } else {
          regex_name.err = ''
          regex_name.valid = true
          this.errors = this.errors.filter(x => x.field !== "name")
          this.errors = [...this.errors, regex_name]
      }
    },
    email: function() {
      let regex_email = this.errors.find(x => x.field === "email")
      if(this.email.match(regex_email.regex) === null) {
        regex_email.err = 'Favor inserir apenas email no formato x@x.x'
        regex_email.valid = false
        this.errors = this.errors.filter(x => x.field !== "email")
        this.errors = [...this.errors, regex_email]
      } else {
        if(regex_email.err !== '') {
          regex_email.err = ''
          regex_email.valid = true
          this.errors = this.errors.filter(x => x.field !== "email")
          this.errors = [...this.errors, regex_email]
        }
      }
    },
    emailConfirm: function() {
      let regex_emailConfirm = this.errors.find(x => x.field === "emailConfirm")
      if(this.email !== this.emailConfirm) {
        regex_emailConfirm.valid = false
        regex_emailConfirm.err = 'Validar os endereços de email'
        this.errors = this.errors.filter(x => x.field !== "emailConfirm")
        this.errors = [...this.errors, regex_emailConfirm]
      } else {
        regex_emailConfirm.err = ''
        regex_emailConfirm.valid = true
        this.errors = this.errors.filter(x => x.field !== "emailConfirm")
        this.errors = [...this.errors, regex_emailConfirm]
      }
      
    },
    pass: function() {
      let regex_pass = this.errors.find(x => x.field === "pass")
      if(this.pass.match(regex_pass.regex) === null) {
        regex_pass.err = 'Favor inserir senha de ao menos 6 caracteres'
        regex_pass.valid = false
        this.errors = this.errors.filter(x => x.field !== "pass")
        this.errors = [...this.errors, regex_pass]
      } else {
        if(regex_pass.err !== '') {
          regex_pass.err = ''
          regex_pass.valid = true
          this.errors.filter(x => x.field !== "pass")
          this.errors = [...this.errors, regex_pass]
        }
      }
    },
    passConfirm: function() {
      let regex_passConfirm = this.errors.find(x => x.field === "passConfirm")
      if(this.pass !== this.passConfirm) {
        regex_passConfirm.err = 'Validar as senhas'
        regex_passConfirm.valid = false
        this.errors = this.errors.filter(x => x.field !== "passConfirm")
        this.errors = [...this.errors, regex_passConfirm]
      } else {
        regex_passConfirm.err = ''
        regex_passConfirm.valid = true
        this.errors = this.errors.filter(x => x.field !== "passConfirm")
        this.errors = [...this.errors, regex_passConfirm]
      }
    },
    errors: function() {
      this.error=0
      this.errors.forEach(x => {
        if(x.valid === false) this.error=1
      })
      if(this.error > 0) this.submitEnable = true
      else               this.submitEnable = false
    }
  },
  methods: {
      validateUser: function(){
        //Validate whether the user already exists
        if (this.userData.length > 0) {
          console.log(this.userData)
          console.log(this.email)
          console.log(this.userData.find(x => x.email === this.email))
            if(this.userData.find(x => x.email === this.email)){
              console.log('aqui')
                this.redirectUserExists('O usuario ja existe. Redirecionando para login...')
            } else {
              this.validateData()
            }
        } else {
            this.validateData()
        }
      },
      validateData: function(){
        if(this.error > 0) this.invalidateUser('Validar todos os campos...')
        else this.createUser()
      },
      invalidateUser: function(text) {
        this.alert = 'show'
        this.alertText = text
      },
      createUser: function() {
        let data = {name: this.name, email: this.email, pass: this.pass}
        this.userData = [...this.userData, data]
        sessionStorage.setItem('userdata', JSON.stringify(this.userData))
        this.alert = 'show'
        this.alertText = 'Login salvo com sucesso!! Redirecionando...'
        setTimeout(() => this.$router.push('/SignIn'), 600)
      },
      redirectUserExists: function(text) {
        this.alert = 'show'
        this.alertText = text
        setTimeout(() => this.$router.push('/SignIn'), 600)
      }
  }
}
</script>