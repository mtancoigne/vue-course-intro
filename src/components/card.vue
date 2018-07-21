<template>
  <div class="card">
    <h1>{{id}}</h1>
    <em>Nom:</em> {{lastName | capitalize}}
    <em>Prénom:</em> {{firstName}}
    <button @click="removeUser">Supprimer</button>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    id: {required: true, type: Number},
    firstName: {required: true, type: String},
    lastName: {required: true, type: String},
  },
  data () {
    return {}
  },
  methods: {
    removeUser () {
      this.$emit('removeMe')
    },
  },
  filters: {
    capitalize: (name) => name.toUpperCase(),
  },
}
</script>

<style scoped> /* Scoped: style limité au composant */
.card {
  border: 1px solid #333;
  margin: 15px 0;
  padding: 10px;
}

h1 {
  color: blue;
}
</style>
