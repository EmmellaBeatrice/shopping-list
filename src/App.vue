<template>
  <div id="app" >
    <header>My Shopping List</header>
    <hr>
    <div id="nav">
      <!-- <router-link to="/">Shopping list</router-link> |
      <router-link to="/addItems">Add Items</router-link> -->
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #d1e7fc;
 
}
header{
  padding-top: 20px;
  font-size: 40px;
  font-weight: bold;
  text-align: left;
  padding-left: 130px;
}
// hr {
//   width: 500px;
//   color: #585383;
// }
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #1c89f7;
    text-decoration: none;
    &.router-link-exact-active {
      color: #1c89f7;
      pointer-events: none;
      opacity: 0.5;
    }
  }
}
</style>
