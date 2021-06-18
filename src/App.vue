<template>
  <div id="app" class="back-dark">
    <div id="nav">
      <router-link to="/">Inicio</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
  </div>
</template>

<script>

</script>

<style>
/* @import "assets/styles/custom.css"; */

body {
  overflow-x: hidden;
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
}

#nav a {
  font-weight: bold;
  color: #e6e8eb;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.back-dark {
  background-color: #404f6b;
}
</style>


