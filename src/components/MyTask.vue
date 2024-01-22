<template>
    <div class="task-layout">
        <span :class="{ 'tache-faite': done }">{{ text }}</span>
        <div class="supprimer">
            <input type="checkbox" :checked="done" @click="onCheck" class="checkbox">
            <button class="button is-danger is-outlined" v-on:click="onRemoveClick">
                <span>Supprimer</span>
            </button>
        </div>
    </div>
</template>
<script>
export default {
    name: 'MyTask',
    props: {
        text: {
            type: String,
            default: ''
        },
        done: {
            type: Boolean,
            default: false
        }
    },
    emits: ['check', 'remove'],
    methods: {
        onRemoveClick() {
            this.$emit('remove');
        },
        onCheck() {
            this.$emit('check');
        }
    }
}
</script>
<style scoped>
.tache-faite {
    transition: all 0.3s;
    text-decoration: line-through;
    color: #48c78e;
}


.task-layout {
    display: grid;
    grid-template-columns: 1fr auto auto;
}
.supprimer{
    display: flex;
    align-items: center;
}


</style>
