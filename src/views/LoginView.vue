<template>
  <div class="container-fluid login-wrapper">
    <div class="login-wrap pt-5">
      <div class="container">
        <div class="row">
          <div class="col-lg-4"></div>
          <div class="col-lg-4 l-side pt-5">
            <h5>
              <strong>PDF Compare</strong>
            </h5>
            <form @submit.prevent="login" class="mt-5">
              <label for="email">Username or email address</label>
              <input
                type="text"
                name="email"
                id="email-field"
                v-model="loginData.email"
                required
              />
              <label for="password">Password</label>
              <input
                type="password"
                name="password"
                id="password-field"
                required
                v-model="loginData.password"
              />

              <button class="mt-4" type="submit">Login</button>
              <div class="rem_lost mt-3">
                <input type="checkbox" name="remember" id="remember" />
                <label for="remember">Remember me</label>
              </div>
              <a href="#" id="lost_pass"> Lost your Password? </a>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loginData: {
        email: "admin@smart.co",
        password: "smarttech",
      },
    };
  },
  methods: {
    login() {
      let email = document.querySelector("#email-field");
      let password = document.querySelector("#password-field");
      if (
        email.value === this.loginData.email &&
        password.value === this.loginData.password
      ) {
        this.$router.push("/app");
      }
    },
  },
};
</script>
