<template>
<div>
<Navigation />
  <div class="container">
  <div class="card" style="padding: 30px">
    <h1>Welcome</h1>
    <h3>Login :</h3>
    <form>
      <div>
        <label for="email">Email</label>
        <input id="email" v-model="email" type="text" name="email" required />
      </div>
      <div>
        <label for="password">Password</label>
        <input
          id="password"
          v-model="password"
          type="password"
          name="password"
          required
        />
      </div>
      <div>
        <button class="btn" type="submit" @click.prevent="login()">
          Login
        </button>
      </div>
    </form>
  </div>
  </div>
</div>
</template>

<script>
import Navigation from "../partials/Navigation";

export default {
  data() {
    return {
      email: null,
      password: null,
    };
  },
  methods: {
    login: function () {
      let email = this.email;
      let password = this.password;

      this.$store
        .dispatch("login", { email, password })
        .then(
          (response) => (
            this.$router.push({ name: "Home" })
          )
        )
        .catch((err) => console.log(err));
    },
  },
  components: {
    Navigation,
  },
};
</script>
