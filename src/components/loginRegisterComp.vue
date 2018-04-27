<template>
  <div>
    <div class="container-fluid">
      <div class = "row firstRow">
        <div class = "registerLogin col-md-3 offset-2">

          <!-- Tab panes -->
          <div class="tab-content">
            <div role="tabpanel" class="tab-pane  in active" id="signIn">
              <form  @submit.prevent="loginSubmit">
                <h2 class="titles">Login</h2>
                <hr/>
                <div class="form-group has-feedback" v-bind:class="[emailSuccessClass]">
                  <label for="email">Email address:</label>
                  <input ref="txtEmail" type="email" class="form-control" @input="checkEmailValidation" id="email" autofocus required>
                </div>
                <div class="form-group has-feedback" v-bind:class="[passwordSuccessClass]">
                  <label for="pwd">Password:</label>
                  <input ref="loginPass" type="password" class="form-control" @input="checkPasswordValidation" id="pwd" required pattern=".{2,10}">
                </div>
                <button v-on:click="loginSubmit" class="btn btn-lg loginButts">Submit</button>
              </form>
            </div>
          </div>
        </div>

        <div class = "registerLogin offset-2 col-md-3 ">
          <div role="tabpanel" class="tab-pane " id="register">
            <form @submit.prevent="registerSubmit">
              <h2 class="titles">Register</h2>
              <hr/>
              <div class="form-group has-feedback has-error" >
                <label for="fName">First Name:</label>
                <input ref="regName" type="text" class="form-control" id="fName" required>
              </div>

              <div class="form-group has-feedback has-error ">
                <label for="sName">Second Name:</label>
                <input ref="regSurname" type="text" class="form-control" id="sName" required>
              </div>

              <div class="form-group has-feedback has-error ">
                <label for="Remail">Email address:</label>
                <input ref="regEmail" type="email" class="form-control"  id="Remail" required>
              </div>
              <div class="form-group has-feedback has-error ">
                <label for="pwdR">Password:</label>
                <input ref="regPass" type="password" class="form-control"  id="pwdR" required>
              </div>

              <button v-on:click="registerSubmit" type="submit" class="btn btn-lg loginButts">Submit</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import mainPage from './mainPage'

  export default {
    name: "loginRegisterComp",
    components: {
      'main-page': mainPage
    },
    data()
    {
      return{
        emailSuccessClass: '',
        passwordSuccessClass: '',
        loginButtonDisable: true,
        component: 'main-page',
      }
    },
    methods: {
      checkEmailValidation: function () {
        if (this.$refs.txtEmail.checkValidity()) {
          this.emailSuccessClass = 'has-success'
        }
        else{
          this.emailSuccessClass = 'has-error'
        }
      },
      checkPasswordValidation: function () {
        if(this.$refs.loginPass.checkValidity())
        {
          this.passwordSuccessClass = 'has-success'
        }
        else {
          this.passwordSuccessClass = 'has-error'
        }
      },
      loginSubmit: function () {
        let email = this.$refs.txtEmail.value.trim();
        let password = this.$refs.loginPass.value.trim();
        let component = this.component;


        if(email !== '' && password !== '')
        {
          this.$emit('loginCred',
            {
              'comp': component,
              'email': email,
              'password': password
            })
        }

      },
      registerSubmit: function () {
        let name = this.$refs.regName.value.trim();
        let surname = this.$refs.regSurname.value.trim();
        let email = this.$refs.regEmail.value.trim();
        let password = this.$refs.regPass.value.trim();
        let component = this.component;

        if(email !== '' && password !== '' && name !== '' && surname !== '')
        {
          this.$emit('registerCred',
            {
              'name': name,
              'surname' : surname,
              'email': email,
              'password': password,
              'comp' : component
            })
        }

      },

    }

  }
</script>

<style scoped>

  .firstRow
  {
    margin-top: 10%;
  }

  .registerLogin
  {
    background: rgba(72, 72, 72, 0.6);
    border-radius: 25px;
    color: #F5F5F5;
    font-family: NanumBarunGothic,serif;
  }

  .tab-content
  {
    padding: 5%;
  }

  #register
  {
    padding: 4%;
  }

  .loginButts
  {
    background: rgba(17, 17, 17, 0.78);
    color:#F5F5F5;

  }

  .loginButts:hover
  {
    background: rgba(170, 170, 170, 0.6);

  }

  hr
  {
    background: white;
  }

  .titles
  {
    font-weight: bolder;
  }

</style>
