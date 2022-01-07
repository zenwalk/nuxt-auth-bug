<template>
  <div class="container">
    <div>
      <h1 class="title">nuxt</h1>
      <h2 class="subtitle">login</h2>
      <nuxt-link to="/">home</nuxt-link>
      <section v-if="this.$auth.loggedIn">
        <h4>Hy {{ this.$auth.user.name }}</h4>
        <p>
          <button @click="interactiveLogout" :disabled="processing">Logout</button>
        </p>
      </section>
      <section v-else>demoauth@nuxt-auth.com | coolToolsGr8Work
        <br>or change axio.baseURL in nuxt.config.js to point to api of yours
        <form @submit.prevent="interactiveLogin">
          <fieldset>
            <p>
              <label>User</label>
              <input v-model="username" type="text" name="username" required>
            </p>
            <p>
              <label>Password</label>
              <input v-model="password" type="password" name="password" required>
            </p>
          </fieldset>
          <p>
            <button type="submit" :disabled="processing">Login</button>
          </p>
        </form>
      </section>
      <h5>after login should take you to default.auth.redirect.home: "/app"</h5>
      <br>
      <h5>after logout should take you to default.auth.redirect.logout: "/"</h5>
    </div>
  </div>
</template>

<script>
// import Logo from '~/components/Logo.vue'

export default {
  // this is the fix
  // thx to Vakrolme https://github.com/nuxt-community/auth-module/issues/437#issuecomment-539528899
  // auth: false,
  components: {},
  data() {
    return {
      processing: false,
      password: "coolToolsGr8Work",
      username: "demoauth@nuxt-auth.com",
      strategy: "local"
      // disableSubmit: false,
    };
  },
  methods: {
    interactiveLogin() {
      this.processing = true;

      this.login({
        username: this.username,
        password: this.password,
        strategy: this.stategy || "local"
      })
        .catch(e => {
          console.error("Error:login() e.response", e.response);
        })
        .finally(() => {
          this.processing = false;
        });
    },
    interactiveLogout() {
      this.processing = true;
      this.logout()
        .catch(e => {
          console.error("Error:logout() e.response", e.response);
        })
        .finally(() => {
          this.processing = false;
        });
    },
    login({
      username = this.username,
      password = this.password,
      strategy = this.stategy || "local"
    }) {
      console.log("login()", this.username, this.password, this.strategy);
      if (!username || !password) {
        throw new Error("Error: username & password are required.");
      }
      // console.debug('store login: %s:%s', email, password)
      if (strategy === "local") {
        // on local strategy we only handle email as username
        return this.$auth.loginWith("local", {
          data: {
            username,
            password
          }
        });
      } else {
        throw new Error(
          `Passport strattegie '${strategy}' isn't supported yet.`
        );
      }
    },
    logout() {
      console.log("logout()");
      return this.$auth.logout();
    }
  }
};
</script>

<style>
</style>
