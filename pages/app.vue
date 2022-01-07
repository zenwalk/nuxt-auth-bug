<template>
  <section>
    <div>
      <h2>App (requires auth)</h2>
      <nuxt-link to="/">Home</nuxt-link>
      <div v-if="this.$auth.loggedIn">
        <p>
           Hi {{ this.$auth.user.name }}
        </p>
        <button @click="logout">Logout</button>
      </div>
      <div v-else>
        <h4>OOOOUUUUPPPPSSSSS</h4>
        This page has auth required.. but you see this as you are not authenticated !!!
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
  },
  middleware: ['auth']
}
</script>

<style></style>
