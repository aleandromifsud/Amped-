<template>
  <div class="hello">
    <component v-bind:is="component" v-on:loginCred="checkCred" v-on:logout="logoutMethod" v-on:registerCred="checkRegister">

    </component>
    <button v-on:click="component = 'main-page'">Show Main</button>
    <button v-on:click="component = 'login-register-comp'">Show Login</button>
    <button v-on:click="spotifyCall"> Test API Call</button>

    <!--<login-register-comp v-on:loginCred="checkCred"></login-register-comp>-->
    <!--<main-page></main-page>-->

  </div>
</template>

<script>
  import loginRegisterComp from './loginRegisterComp'
  import mainPage from './mainPage'
  import SpotifyWebApi from "spotify-web-api-node";

  export default {
    name: 'HelloWorld',
    components: {
      'login-register-comp': loginRegisterComp,
      'main-page': mainPage

    },
    data () {
      return {
        component: 'login-register-comp'
      }
    },
    methods: {
      checkCred: function (event) {
        this.component = event.comp;
        console.log("Entered Email :"+event.email);
        console.log("Entered Password : "+event.password);
      },
      checkRegister: function (event) {
        this.component = event.comp;
        console.log("Entered Email :"+event.email);
        console.log("Entered Password : "+event.password);
        console.log("Entered Name : "+event.name);
        console.log("Entered Surname : "+event.surname);
      },
      spotifyCall: function () {


        // const spotifyApi = require('SpotifyWebApi');
        // const SpotifyWebApi = new spotifyApi('840a8b7f99994b33994d3b2706725d6f');

        const spotifyApi = new SpotifyWebApi({
          clientId : ' 840a8b7f99994b33994d3b2706725d6f',
          clientSecret : '4eb59e91ee894ca99fa52289f3cee09d',
          redirectUri : 'index.html'
        });

        //spotifyApi.setAccessToken('BQB4FMtMM03ZgWx30XVPoXmm_nvjEgr0PtjxqjNDwT_ZyHag0_uUh7ja2MKuVN8sxmdGHLl1pWEjbFE7qgD9GYJaALt7fooERe9fzZ5JcZaTDIVYqaKxS02JqNtESVZU73avyRdNJOQDiEyoJ8V-hLbgz8SZ33hjWqXqCAOiH0gU');

        spotifyApi.getArtistAlbums('43ZHCT0cAZBISjO8DG9PnE')
          .then(function(data) {
            console.log('Artist albums', data.body);
          }, function(err) {
            console.error(err);
          });

      },
      logoutMethod : function (event) {
        this.component = event.comp;
        console.log("User Logged Out");
        console.log("Changing Component To : "+event.comp);
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
