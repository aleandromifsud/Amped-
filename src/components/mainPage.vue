<template>
  <div>
    <nav class="navbar navbar-fixed-bottom navbar-expand-sm bg-inverse ">
      <div class = "container-fluid">

        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#nav-content" aria-controls="nav-content" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>

        <!-- Brand -->
        <a class="navbar-brand" href="#">
          <img src="../assets/logo/logo.png" class="d-inline-block align-top" alt="">
        </a>

        <!-- Links -->
        <div class="collapse navbar-collapse justify-content-end" id="nav-content">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link" href="#"><span class="fas fa-user"></span><span class="nav-label"> User</span></a>
            </li>
            <li class="nav-item">
              <button class="nav-link" type="submit" v-on:click="logoutMethod"><span class="fas fa-sign-out-alt"></span><span class="nav-label"> Logout</span></button>
            </li>
          </ul>
        </div>

      </div>
    </nav>

    <nav class="navbar-primary">
      <a v-on:click="moveMenu" href="#" class="btn-expand-collapse"><span class="fas fa-angle-double-left"></span></a>
      <ul class="navbar-primary-menu">
        <li>
          <a href="#"><span class="fas fa-music"></span><span class="nav-label"> New Music</span></a>
          <a href="#"><span class="fas fa-fire"></span><span class="nav-label"> Popular</span></a>
          <a href="#"><span class="far fa-save"></span><span class="nav-label"> Saved</span></a>
        </li>
      </ul>
    </nav>
  </div>

</template>

<script>
  import loginRegisterComp from './loginRegisterComp'

  export default {
    name: "main-page",
    components: {
      'login-register-comp': loginRegisterComp
    },
    data()
    {
      return{
        component: 'login-register-comp'
      }
    },
    methods: {
      moveMenu : function () {
        $('.navbar-primary').toggleClass('collapsed');
      },
      logoutMethod: function ()
      {
        let component = this.component;

        this.$emit('logout',
          {
            'comp': component,
          })


      }
    }
  }
</script>

<style scoped>
  .navbar-primary {
    background-color: #333;
    bottom: 0px;
    left: 0px;
    position: fixed;
    top: 75px;
    width: 200px;
    z-index: 8;
    overflow: hidden;
    -webkit-transition: all 0.1s ease-in-out;
    -moz-transition: all 0.1s ease-in-out;
    transition: all 0.1s ease-in-out;
  }

  .navbar-primary.collapsed {
    width: 60px;
  }

  .navbar-primary.collapsed{
    font-size: 22px;
  }

  .navbar-primary.collapsed .nav-label {
    display: none;
  }

  .btn-expand-collapse {
    position: absolute;
    display: block;
    left: 0;
    bottom:0;
    width: 100%;
    padding: 8px 0;
    border-top:solid 1px #666;
    color: grey;
    font-size: 20px;
    text-align: center;
  }
  #nav-content a:hover,
  #nav-content a:focus,
  .btn-expand-collapse:hover,
  .btn-expand-collapse:focus {
    background-color: #222;
    color: white;
  }

  .btn-expand-collapse:active {
    background-color: #111;
  }

  .navbar-primary-menu,
  .navbar-primary-menu li {
    margin:0; padding:0;
    list-style: none;
  }

  .navbar-primary-menu li a {
    display: block;
    padding: 10px 18px;
    text-align: left;
    border-bottom:solid 1px #444;
    color: #ccc;
  }

  .navbar-primary-menu li a:hover {
    background-color: #2e2e2e;
    text-decoration: none;
    color: white;
  }

  .navbar-primary-menu li a{
    margin-right: 6px;
  }

  .nav-link
  {
    color: white;
    background: transparent;
    border-color: transparent;
  }

  .nav-link:hover
  {
    background-color: #2e2e2e;
    color: white;
    border: 0.5px solid #2f2f2f;
  }

  .main-content {
    margin-top: 1.8%;
    margin-left: 10%;
    padding: 20px;
    color: white;

  }

  .collapsed + .main-content {
    margin-left: 60px;
  }

  .bg-inverse
  {
    background-color: #333;

  }

  #nav-content a
  {
    color: #ccc;
  }


</style>
