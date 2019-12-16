<template>
  <div class="login">
    <form @submit="logIn">
      <div class="input-area">
        <p class="welcome">
          Welcome to <br /><span style="text-decoration: underline">rem</span
          >inStore<br />
          BI tool.
        </p>
        <div class="inputs">
          <div class="username">
            <label class="input-label">Username</label><br />
            <input
              type="text"
              class="user-input"
              v-model="username"
              placeholder="Enter your username"
              required
            />
          </div>
          <div class="password">
            <label class="input-label">Password</label><br />
            <input
              type="password"
              class="pass-input"
              placeholder="Enter your password"
              v-model="password"
              required
            />
          </div>
        </div>
        <button type="submit" class="login-btn">Login</button>
      </div>
    </form>
  </div>
</template>

<script>
import Vue from "vue";
import VueNoty from "vuejs-noty";
import "vuejs-noty/dist/vuejs-noty.css";

Vue.use(VueNoty, {
  timeout: 500,
  progressBar: false,
  layout: "topRight"
});

export default {
  data() {
    return {
      username: "",
      password: "",
      users: [
        { username: "Yavuz", password: "123" },
        { username: "Selim", password: "123" }
      ],
      isValid: null,
      message: "Incorrect username or password",
      errors: []
    };
  },
  beforeCreate: function() {
    document.body.className = "home";
  },
  methods: {
    logIn(e) {
      this.isValid =
        this.users.filter(
          x => x.username == this.username && x.password == this.password
        ).length == 1;

      if (this.isValid) {
        this.$router.push("/table");
        this.$noty.success("You're logged in!");
      } else this.$noty.error("Incorrect username or password");
      this.errors = [];

      e.preventDefault();
    }
  }
};
</script>

<style scoped>
.input-area {
  max-width: 100%;
}

.inputs:after {
  clear: both;
}

.inputs > div {
  min-height: 60px;
  float: left;
  margin-right: 30px;
  box-shadow: 0px 6px 5px 2px rgb(119, 120, 123);
}

.username {
  background: #fff;
  text-align: left;
  border-radius: 6px;
}

.password {
  background: #fff;
  text-align: left;
  border-radius: 6px;
}

@media all and (max-width: 700px) {
  .inputs > div {
    float: none;
    margin-bottom: 30px;
  }
}

.login {
  display: flex;
  align-items: center;
  justify-content: center;
  float: left;
  margin-top: 150px;
  margin-left: 100px;
}

.welcome {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-size: 36px;
  text-align: left;
  color: #000;
}

.login-btn {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  float: right;
  margin-top: 25px;
  font-weight: bold;
  border-radius: 0;
  background-color: #fff;
  border-color: rgba(191, 27, 109, 0.88);
  border-radius: 3px;
  width: 85px;
  height: 35px;
  color: #ff69b4;
  font-size: 16px;
  -webkit-box-shadow: 0px 0px 10px 3px rgba(191, 27, 109, 0.88);
  box-shadow: 0px 0px 10px 3px rgba(191, 27, 109, 0.88);
  margin-right: 30px;
}

.pass-input,
.user-input {
  border: none;
  width: 294px;
  height: 40px;
  font-size: 13px;
  padding-left: 5px;
  border-radius: 6px;
}

.input-label {
  font-size: 11px;
  padding-left: 5px;
}
</style>
