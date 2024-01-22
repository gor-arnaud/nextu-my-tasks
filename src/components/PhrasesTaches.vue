<template>
    <div class="bilan">
      Vous avez terminé <span id="TachesFini"> {{ TachesFini }}</span> tâche dans votre liste qui compte<span v-if="TachesFini !== 1">s</span> {{ TachesTotal }}.
    </div>
</template>

<script>
export default {
    name: 'PhrasesTaches',
    props: {
        taches: {
            type: Array,
            required: true
        }
    },
    computed: {
        TachesTotal() {
            return this.taches.length;
        },
        TachesFini() {
            return this.taches.filter(tache => tache.fait).length;
        }
    }
}
</script>
<style>
#TachesFini{
    color: #48c78e;
    font-weight: 500;

}
</style>
