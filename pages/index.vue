<template>
  <section>
    <div>
      <nuxt-link to="/">Home</nuxt-link>
      <nuxt-link to="/app">App</nuxt-link>

      <nuxt-link to="/callback">Callback (try me before login to see...)</nuxt-link>
      <p>
        then try again uncommenting callback in nuxt.config.js
        <br />
        (seems same happens when logout: points to a page requireing auth)
      </p>
      <div v-if="this.$auth.loggedIn">
        <p>
           Hi {{ this.$auth.user.name }}
        </p>
        <button @click="logout">Logout</button>
      </div>
      <div v-else>
        <nuxt-link to="/login">Login</nuxt-link>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  components: {
  },
  methods: {
    logout () {
      return this.$auth.logout()
    }
  }
}
</script>

<style></style>
