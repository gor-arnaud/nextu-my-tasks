<template id="template">
  <div id="app">
    <h1>Ma liste de tâches</h1>
    
    <ul v-if="afficher">
        <li v-for="(tache, index) in taches" :key="index">
          <ul>
            <div class="listes">
              <my-task v-bind:text="tache.nom" v-bind:done="tache.fait" @remove="onTaskRemove(index)" v-on:check="onTaskCheck(index, $event)">
              </my-task>
            </div>
          </ul>
        </li>
    </ul>
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
    <phrases-taches :taches="taches" id="phrases-taches"></phrases-taches>
  </div>
</template>

<script>
import MyTask from './components/MyTask.vue';
import PhrasesTaches from './components/PhrasesTaches.vue';


export default {
  name: 'App',
  components: {
    MyTask,
    PhrasesTaches
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
<style>
#phrases-taches{
  width: 55%;
  font-size: 30px;
  border: 2px solid black;
  text-align: center;
  margin-left: 23%;
  border-radius: 20px;
}
#app{
  margin: 2% 2%;
}
#app h1{
  text-align: center;
  font-size: 30px;
  font-weight: bold;
}
.button{
  margin-top: 30px;
}
.checkbox{
  margin-top: 30px;
    margin-right: 10px;

}
.listes span{ 
  font-weight: bold;
  display: flex;
  align-items: center;
  transition: all 0.3s;
    color: #f14668;
}
.is-danger :hover{
  transition: all 0.3;
  color: white;
}
.task-layout {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

</style>
