<template>
  <div id="app">
    <h1>Titre</h1>
    <one-card class="super"
              :id="u.id"
              :first-name="u.firstName"
              :last-name="u.lastName"
              :v-key="u.id"
              @removeMe="removeUser(u.id)"
              v-for="u in users"/>
  </div>
</template>

<script>
import Card from './components/card'
import users from './fakedata'

export default {
  name: 'App',
  components: {OneCard: Card},
  data () {
    return {
      // Equivalent de :
      // users: user,
      users,
    }
  },
  methods: {
    removeUser (id) {
      for (let i in this.users) {
        if (this.users[i].id === id) {
          this.users.splice(i, 1)
          break
        }
      }
    },
  },
}
</script>

<style>
  h1 {
    color: red;
    font-size: 2em;
  }
</style>
