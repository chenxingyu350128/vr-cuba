<template>
  <div id="app">
    <about />
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view style="height: 100%;" /> -->
  </div>
</template>
<script>
import About from './views/About.vue';
export default {
  name: 'VrCubaApp',
  components: {
    About
  }

};
</script>
<style lang="scss">
html, body, #app {
  height: 100vh;
  padding: 0;
  margin: 0;
  overflow: hidden;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
