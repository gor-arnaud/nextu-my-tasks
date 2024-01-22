<template>
    <div class="bilan">
      <p>
        Vous avez terminé
        <span :class="{ 'text-success': TachesFini > 0 }">
          {{ TachesFini }}
        </span>
        tâche{{ TachesFini !== 1 ? 's' : '' }} sur un total de {{ TachesTotal }}.
      </p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'PhrasesTaches',
    props: {
      taches: {
        type: Array,
        required: true,
      },
    },
    computed: {
      TachesTotal() {
        return this.taches.length;
      },
      TachesFini() {
        return this.taches.filter((tache) => tache.fait).length;
      },
    },
  };
  </script>
  
  <style scoped>
  .text-success {
    color: green;
    font-weight: bold;

  }

#TachesFini{
    color: #48c78e;
}
</style>
