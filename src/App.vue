<template>
  <div id="app">
    <nav class="navbar">
      <router-link to="/">Home</router-link> |
      <router-link to="/map">Map</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<style>
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  padding: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.navbar {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
  margin-bottom: 2rem;
  background: #F0F0F0;
}
.navbar a {
  font-weight: bold;
  color: #2c3e50;
  padding: 0 0.5rem;
}
.navbar a.router-link-exact-active {
  color: #42b983;
}
</style>
