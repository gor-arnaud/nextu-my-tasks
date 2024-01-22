<template>
    <div class="total">
        You finished {{ tacheFini }} task<span v-if="tacheFini !== 1">s</span> on {{ tacheTotal }}.
    </div>
</template>

<script>
    export default {
        name : 'Sentece',
        props: {
            taches: {
                type: Array,
                requiered: true,
            }
        },
        computed: {
        tacheTotal() {
            return this.taches.length;
            }, 
        tacheFini() {
            return this.taches.filter (tache => tache.fait).length; 
            }
        }
    
    }
</script>