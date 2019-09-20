<template>
  <div class="font">
    <form v-if="loginForm" @submit.prevent="loginUser">
      <input type="email" v-model="creds.email" placeholder="email" />
      <input type="password" v-model="creds.password" placeholder="password" />
      <button class="login-button">Login</button>
    </form>
    <form v-else @submit.prevent="register">
      <input type="text" v-model="newUser.name" placeholder="name" />
      <input type="email" v-model="newUser.email" placeholder="email" />
      <input type="password" v-model="newUser.password" placeholder="password" />
      <button class="login-button">Create Account</button>
    </form>
    <div class="action text-color" @click="loginForm = !loginForm">
      <p v-if="loginForm">
        <b>No account? Click here to Register</b>
      </p>
      <p v-else>
        <b>Already have an account? Click here to Login</b>
      </p>
    </div>
  </div>
</template>

<script>
import router from "@/router.js";
export default {
  name: "login",
  data() {
    return {
      loginForm: true,
      creds: {
        email: "",
        password: ""
      },
      newUser: {
        email: "",
        password: "",
        name: ""
      }
    };
  },
  beforeCreate() {
    if (this.$store.state.user._id) {
      this.$router.push({ name: "boards" });
    }
  },
  methods: {
    register() {
      this.$store.dispatch("register", this.newUser);
    },
    loginUser() {
      this.$store.dispatch("login", this.creds);
    }
  }
};
</script>

<style>
.action {
  cursor: pointer;
}
.text-color {
  color: #908a99;
}
.font {
  font-family: "Press Start 2p";
  font-size: 10px;
}
.login-button {
  display: inline-block;
  padding: 3px 8px;
  font-size: 15px;
  text-align: center;
  outline: none;
  color: #fff;
  background-color: #b5b6e4;
  border: none;
  border-radius: 15px;
  box-shadow: 0 5px #606188;
}
.login-button:hover {
  background-color: #a4a5d3;
}
.login-button:active {
  background-color: #8d8ebe;
  box-shadow: 0 3px #606188;
  transform: translateY(4px);
}
.login-button:focus {
  outline: 0;
}
</style>