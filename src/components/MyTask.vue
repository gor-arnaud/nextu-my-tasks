<template>
    <div class="task-layout">
        <span :class="{ 'tache-faite': done }">{{ text }}</span>
        <input type="checkbox" :checked="done" @click="onCheck" class="checkbox">
        <button class="button is-danger is-outlined" v-on:click="onRemoveClick">
            <span>Supprimer</span>
        </button>
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
    text-decoration: line-through;
}

.task-layout {
    display: grid;
    grid-template-columns: 1fr auto auto;
}
.button.is-danger.is-outlined:hover {
    background-color: #DC143C; 
    color: white; 
}
</style>
