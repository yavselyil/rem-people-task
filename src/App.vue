<template>
  <div id="app">
    <div v-if="!isLoginPage" id="nav">
      <router-link to="/table">Table</router-link> |
      <router-link to="/chart">Chart</router-link>
    </div>
    <router-view />
  </div>
</template>

<script>
export default {
  computed: {
    isLoginPage() {
      return this.$route.name == "home";
    }
  }
};
</script>

<style lang="scss">
body.table {
  background-image: url("assets/background.png");
}
body.chart {
  background-image: url("assets/background.png");
}
body.home {
  background-image: url("assets/login.png");
  background-size: cover;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: 100%;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: 100% 100%;
  width: 100%;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    padding: 5px;
    border: 1px solid rgba(255, 255, 255, 0.5);
    font-weight: bold;
    color: #f5f5f5;
    text-decoration: none;

    &.router-link-exact-active {
      color: #f5f5f5;
      background-color: rgba(191, 27, 109, 0.88);
      -webkit-box-shadow: 0px 0px 10px 3px rgba(191, 27, 109, 0.88);
      box-shadow: 0px 0px 10px 3px rgba(191, 27, 109, 0.88);
    }
  }
}
</style>
