<template>
  <div id="app">
    <div id="nav">
      <!-- <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> -->
      <span>New Uzbekistan Pizza</span>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
#nav {
  margin: 0 auto;
  padding: 30px;
  display: flex;
  justify-content: center;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }

  span {
    font-size: 20px;
    font-weight: bold;
    letter-spacing: 1px;
  }
}



</style>
