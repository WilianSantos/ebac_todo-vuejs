<script setup>
    const props = defineProps(['tarefas']);
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="evento => tarefa.concluida = evento.target.checked" :checked="tarefa.concluida" :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.concluida }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
        </li>
    </ul>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }
</style>