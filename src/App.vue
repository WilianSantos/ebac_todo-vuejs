<script setup>

import { reactive } from 'vue';

  const estado = reactive({
    tarefas: [
      { titulo: 'Estudar ES', concluida: false },
      { titulo: 'Estudar Vue', concluida: true },
      { titulo: 'Estudar React', concluida: false },
      { titulo: 'Estudar Angular', concluida: false },
      { titulo: 'Estudar Node', concluida: false },
      { titulo: 'Estudar Java', concluida: false },
      { titulo: 'Estudar Python', concluida: false },
    ],
    filtro: 'todas',
    tarefaTemp: '',
  });

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.concluida);
  }

  const getTarefasConcluidas = () => {
    return estado.tarefas.filter(tarefa => tarefa.concluida);
  }

  const getTarefasFiltardas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'concluidas':
        return getTarefasConcluidas();
      default:
        return estado.tarefas;
    }
  }

  const cadrastaTarefa = () => {

    estado.tarefas.push({
      titulo: estado.tarefaTemp,
      concluida: false,
    });

    estado.tarefaTemp = '';
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>
    
    <form @submit.prevent="cadrastaTarefa">
      <div class="row">
        <div class="col">
          <input type="text" :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" placeholder="Digite aqui a descrição da sua tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select class="form-control" @change="estado.filtro = $event.target.value">
            <option value="todas">Todas</option>
            <option value="pendentes">Pendentes</option>
            <option value="concluidas">Concluídas</option>
          </select>
        </div>
      </div>
    </form>

    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltardas()">
        <input @change="evento => tarefa.concluida = evento.target.checked" :checked="tarefa.concluida" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.concluida }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
      </li>
    </ul>
  </div>
  
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
