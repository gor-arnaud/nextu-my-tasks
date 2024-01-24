<template>
  <div id="app">
    <h1>Ma liste de tâches</h1>
    <ul v-if="afficher">
      <li v-for="(tache, index) in taches" :key="index">
        <ul>
          <my-task v-bind:text="tache.nom" v-bind:done="tache.fait" @remove="onTaskRemove(index)" v-on:check="onTaskCheck(index, $event)">
          </my-task>
        </ul>
      </li>
    </ul>
    <exo-num :taches="taches"></exo-num>
    <button v-on:click="afficher = true" v-if="!afficher" class="button">
      Afficher vos tâches
    </button>
    <button v-on:click="afficher = false" v-else class="button">
      Masquer vos tâches
    </button>
    <br />
    <label>Nouvelle tâche</label><input type="text" v-model="nouvelleTache" class="input">
    <button class="button is-success" v-on:click="ajouterTache">
      <span>Nouvelle tâche</span>
    </button>
  </div>
</template>

<script>
import ExoNum from './components/ExoNum.vue';
import MyTask from './components/MyTask.vue';

export default {
  name: 'App',
  components: {
    MyTask,
    ExoNum
},
  data() {
    return {
      taches: [
        { nom: 'faire les courses', fait: false },
        { nom: 'étendre la lessive', fait: true },
        { nom: 'faire un top 1 à Fortnite', fait: false },
      ],
      afficher: true,
      nouvelleTache: '',
    }
  },
  methods: {
    ajouterTache() {
      this.taches.push({ nom: this.nouvelleTache, fait: false });
      this.nouvelleTache = '';
    },
    onTaskRemove(index) {
      this.taches.splice(index, 1);
    },
    onTaskCheck(index, event) {
      this.taches[index].fait = !this.taches[index].fait;
      console.log('check event: ', event);
    }
  }
}
</script>
