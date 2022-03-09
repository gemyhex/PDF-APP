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

<style lang="scss" scoped>
.login-wrapper {
  .page-head {
    position: relative;
    padding: 0;
    height: 400px;
    .breadcrumb {
      background: transparent;
      li {
        a {
          color: white;
          font-weight: bold;
        }
      }
    }
    .overlay {
      .cont {
        position: absolute;
        bottom: 40%;
        left: 15%;
        color: #fff;
        h2 {
          font-size: 3rem;
          font-weight: bolder;
          span {
            color: red;
          }
        }
        p {
          font-weight: bold;
        }
      }
    }
  }
  .login-wrap {
    height: 600px;
    h5 {
      font-size: 2rem;
      font-weight: 600;
    }
    p {
      a {
        color: #000;
        font-weight: 600;
      }
    }
    .l-side {
      height: fit-content;
      label {
        display: block;
        font-weight: bold;
        // margin-top: 15px;
      }
      input {
        width: 100%;
        height: 40px;
        padding: 8px 15px;
        font-weight: bold;
      }
      button {
        width: 100%;
        height: 40px;
        font-weight: bold;
        color: #fff;
        background: red;
        border: none;
      }
      .rem_lost {
        display: flex;
        justify-content: center;
        align-items: center;
        input {
          width: 18px;
          height: 18px;
          float: left;
          border: none;
          background: #a8a8a8;
          margin-right: 5px;
        }
        label {
          padding-left: 10px;
        }
      }
      #lost_pass {
        color: #000;
        font-weight: bold;
      }
    }
  }
}
</style>
