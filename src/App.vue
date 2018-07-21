<template>
  <div id="app">
    <ul>
      <li><a href="#" @click.prevent="tab = 'partie1'">Partie 1 : Intro, variables, méthodes, boucles et conditions</a>
      <li><a href="#" @click.prevent="tab = 'partie2'">Partie 2 : Composants</a></li>
      <li><a href="#" @click.prevent="tab = 'partie3'">Partie 3 : Vue-resource et slots</a></li>
    </ul>

    <partie1 v-if="tab === 'partie1'"/>
    <partie2 v-if="tab === 'partie2'"/>
    <partie3 v-if="tab === 'partie3'"/>

  </div>
</template>

<script>
import Partie1 from './Partie1'
import Partie2 from './Partie2'
import Partie3 from './Partie3'

export default {

  name: 'App',
  components: {Partie1, Partie2, Partie3},
  data () {
    return {
      tab: 'partie1',
    }
  },
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
  }
</style>
