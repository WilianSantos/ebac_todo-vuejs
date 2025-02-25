<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'filtro', 'editaTarefaTemp']);
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
            <input type="text" :value="props.tarefaTemp" @change="props.editaTarefaTemp" placeholder="Digite aqui a descrição da sua tarefa" class="form-control">
            </div>
            <div class="col-md-2">
            <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
            <select class="form-control" @change="props.filtro">
                <option value="todas">Todas</option>
                <option value="pendentes">Pendentes</option>
                <option value="concluidas">Concluídas</option>
            </select>
            </div>
        </div>
    </form>
</template>