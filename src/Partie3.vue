<template>
  <div id="app">
    <h1>Posts:
      <button @click="getPosts">Reload !</button>
    </h1>

    <!-- Ajouté après le cours pour afficher les erreurs -->
    <pre style="color: red" v-if="error">{{error}}</pre>

    <!--
    Formulaire. ".prevent" permet que le navigateur n'execute pas son
    action par défaut (envoyer le formulaire, donc recharger la page) -->
    <form @submit.prevent="createPost">
      <div>
        <label for="title">Titre</label>
        <input id="title" type="text" v-model="inputs.title">
      </div>
      <div>
        <label for="content">Contenu</label>
        <textarea name="content" id="" cols="30" rows="10" v-model="inputs.content"></textarea>
      </div>
      <input type="submit">
    </form>

    <div v-if="loading">Chargement en cours</div>
    <div v-else>
      <div v-for="p in dataFromAPI">
        <div><em>title:</em> {{p.title}}</div>
        <div><em>content:</em> {{p.content}}</div>
        <div><em>createdAt:</em> {{p.createdAt}}</div>
        <div><em>updatedAt:</em> {{p.updatedAt}}</div>
        <div><em>id:</em> {{p.id}}</div>
      </div>
    </div>

    <!-- Les slots ----------------------------------------------------->
    <h2>Composant avec slot :</h2>
    <composant-avec-slot>Ceci est dans le slot</composant-avec-slot>

  </div>
</template>

<script>
import ComposantAvecSlot from './components/avec-slot'

const API_URL = 'http://localhost:1337'

export default {
  name: 'App',
  components: {ComposantAvecSlot},
  data () {
    return {
      dataFromAPI: [],
      loading: false,
      inputs: {
        title: '',
        content: '',
      },
      // Ajouté après le cours pour afficher les erreurs de l'api
      error: null,
    }
  },
  methods: {
    getPosts () {
      // On définit l'état comme étant "en train de charger".
      this.loading = true
      // Lancement de la requête avec Vue Resource
      this.$http.get(`${API_URL}/posts`) // Renvoie une "Promise"
      // On effectue quelque chose avec le retours de la promise réussie
      // (en cas de réussite seulement)
        .then(({body}) => {
          this.dataFromAPI = body
        })
        // On effectue quelque chose avec le retours d'échec de la promise
        // (en cas d'echec seulement)
        .catch((error) => {
          console.error(error)
          this.error = error
        })
        // Pour finir, on dit que l'on n'est plus en train de charger.
        .then(() => {this.loading = false})
    },
    createPost () {
      this.loading = true
      const payload = this.inputs
      this.$http.post(`${API_URL}/posts`, payload)
        .then(({body}) => {this.dataFromAPI.push(body)})
        .catch((error) => {
          console.error(error)
          this.error = error
        })
        .then(() => {this.loading = false})
    },
  },
  created () {
    // Récupération des posts au chargement
    this.getPosts()
  },
}
</script>
