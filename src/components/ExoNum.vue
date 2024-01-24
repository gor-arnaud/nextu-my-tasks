<template>
    <div class="total">
        Vous avez accomplis {{ tacheFaite }} tâche <span v-if="tacheFaite !== 1">s</span> sur un total de {{ nbTaches }},
    </div>
</template>

<script>
import { computed } from 'vue';

export default{
    name: 'TacheFini',
    props: {
        taches: {
            type: Array,
            required: true
        }
    },
    computed :{
        nbTaches(){
            return this.taches.length;
        },
        tacheFaite(){
            return this.taches.filter(tache => tache.fait).length;
        }
    }
}

</script>