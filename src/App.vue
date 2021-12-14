<template>
  <div class="mainContent">
    <header>
      <div class="container-nav">
        <div class="container-logo">
          <img src="./assets/logo.svg" alt="" />
        </div>
        <div id="nav">
          <a class="a" to="/">Home</a>
          <a class="a" to="/features">Features</a>
          <a class="a" to="/pricing">Pricing</a>
          <a class="a" to="/pricing">Ressources</a>
        </div>
      </div>

      <div class="container-btn">
        <button>Login</button>
        <button>Sign Up</button>
      </div>
    </header>

    <p>
      Voici mon url:
      <input type="text"  v-on:keyup.enter="getShortedUrl($event)" />
    </p>

    <p>Link1: <a :href="'https://'+url" target="_blank">{{url}}</a></p>

  </div>
  <router-view />
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      url: null,
      urlToShortcut:null

    };
  },
  methods: {
    getShortedUrl(e){

      axios.get("https://api.shrtco.de/v2/shorten?url="+e.target.value).then((res) => {

      console.log(res)
      this.url = res.data.result.short_link
      })
    }
  },

  computed:{
    getUrlLink1(){
      return this.url.short_link
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
header {
  display: flex;
  justify-content: space-between;

  width: 80vw;
  .container-nav {
    display: flex;
    width: 90%;
    #nav {
      width: 40%;
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      // border: 2px solid;
      padding: 30px;

      .a {
        text-decoration: none;
        color: gray;
        // border: 2px solid;
      }
      a {
        font-weight: bold;
        color: #2c3e50;

        &.a-exact-active {
          color: #42b983;
        }
      }
    }
  }
  .container-btn {
    width: 10%;
    display: flex;
    justify-content: space-between;
    button:first-child {
      background-color: white;
      color: gray;
      padding: 5px 10px;
    }
    button:nth-child(2) {
      background-color: rgb(43, 209, 207);
      border-radius: 30px;
      color: white;
      padding: 5px 10px;
    }
    button {
      height: fit-content;
      border: none;
    }
  }
}
</style>
