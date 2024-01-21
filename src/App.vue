<template>
  <div id="app">
    <h1>Ma liste de tâches</h1>
    <ul v-if="afficher">
      <li v-for="(tache, index) in taches" :key="index">
        <ul>
          <my-task 
            v-bind:text="tache.nom" 
            v-bind:done="tache.fait" 
            @remove="onTaskRemove(index)" 
            v-on:check="onTaskCheck(index, $event)">
          </my-task>
        </ul>
      </li>
    </ul>
    <phrase-bilan :taches="taches"></phrase-bilan>
    <div style="height: 20px;"></div>
    <button v-on:click="afficher = true" v-if="!afficher" class="button">
      Afficher vos tâches
    </button>
    <button v-on:click="afficher = false" v-else class="button">
      Masquer vos tâches
    </button>
    <div style="height: 20px;"></div> 
    <br />
    <label> Nouvelle tâche </label><input type="text" v-model="nouvelleTache" class="input" @input="clearErrorMessage">
    <button class="button is-success" v-on:click="ajouterTache">
      <span>Nouvelle tâche</span>
    </button>
    <div v-if="errorMessage" class="error-message">{{ errorMessage }}</div>
</div>
</template>

<script>
import MyTask from './components/MyTask.vue';
import PhraseBilan from './components/PhraseBilan.vue'; 

export default {
  name: 'App',
  components: {
    MyTask,
    PhraseBilan
  },
  data() {
    return {
      taches: [
        { nom: 'Faire les courses', fait: false },
        { nom: 'Étendre la lessive', fait: true },
        { nom: 'Faire un top 1 à Fortnite', fait: false },
      ],
      afficher: true,
      nouvelleTache: '',
      errorMessage: '',
    }
  },
  methods: {
    ajouterTache() {
      if (this.nouvelleTache.trim() === '') {
      this.errorMessage = 'Veuillez entrer le nom de la tâche.';
      return;
    }
      this.taches.push({ nom: this.nouvelleTache, fait: false });
      this.nouvelleTache = '';
    },
    onTaskRemove(index) {
      this.taches.splice(index, 1);
    },
    onTaskCheck(index, event) {
      this.taches[index].fait = !this.taches[index].fait;
      console.log('check event: ', event);
    },
    clearErrorMessage() {
    if (this.errorMessage) {
      this.errorMessage = '';
    }
  },

  }
}
</script>
<style>
  .error-message {
    color: #DC143C;
    margin-top: 10px;
  }
</style>
