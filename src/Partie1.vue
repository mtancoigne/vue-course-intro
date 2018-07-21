<template>
  <div id="app">
    {{counter}}
    <button @click="removeOne" :disabled="counter === 0">-</button>
    <button @click="addOne" v-if="counter < 10">+</button>
    <span v-else>10 c'est suffisant</span>
    <hr>

    <pre>{{message}}</pre>

    <button v-for="letter in alphabet" @click="addLetter(letter)">{{letter}}</button>

    <form action="" @submit.prevent="formulaire">

      <textarea @keyup.enter="formulaire2"></textarea>
      <input type="submit">
    </form>
  </div>
</template>

<script>
export default {
  name: 'App',
  // Liste de propriétés passables au composant
  props: {},
  // Liste de composants
  components: {},
  // "Variables" disponibles dans la vue
  data () {
    return {
      counter: 0,
      alphabet: 'abcdefghijklmnopqrstuvwxyz',
      message: '',
    }
  },
  // Méthodes du composant
  methods: {
    addLetter (l) {
      this.message += l
    },
    removeOne () {
      if (this.counter > 0) {
        this.counter--
      }
    },
    addOne () {
      this.counter++
    },
    formulaire(){
      this.message = 'Formulaire envoyé'
    },
    formulaire2(){
      this.message = 'Touche pressée'
    }
  },
  // Propriétés "réactives" (sous forme de méthodes)
  computed: {},
  // Executée quand le composant est créée
  created () {},
  // Est éxecutée quand le composant est ajouté au DOM
  mounted () {},
  // ...
  // Actions à réaliser sur des changements de variables
  watch: {},
  // Méthodes "hors scope", disponibles dans la vue uniquement
  filters: {
    plusTen: (val) => val + 10,
  },
}
</script>
