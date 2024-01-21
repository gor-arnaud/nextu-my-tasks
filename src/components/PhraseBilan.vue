<template>
    <div class="bilan">
      Vous avez terminé {{ nombreFini }} tâche<span v-if="nombreFini !== 1">s</span> sur un total de {{ nombreTotal }}.
    </div>
  </template>
  
  <script>
  export default {
    name: 'PhraseBilan',
    props: {
      taches: {
        type: Array,
        required: true
      }
    },
    computed: {
      nombreTotal() {
        return this.taches.length;
      },
      nombreFini() {
        return this.taches.filter(tache => tache.fait).length;
      }
    }
  }
  </script>
  
  <style scoped>
  .bilan {
    margin-top: 100px;
    font-weight: bold;
  }
  </style>
  