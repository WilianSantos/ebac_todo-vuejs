<script setup>

import { reactive } from 'vue';

import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefa from './components/ListaDeTarefa.vue';

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

    const cadastraTarefa = () => {

        estado.tarefas.push({
        titulo: estado.tarefaTemp,
        concluida: false,
        });

        estado.tarefaTemp = '';
    }
</script>

<template>
    <div class="container">
        <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
        <Formulario :filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
        <ListaDeTarefa :tarefas="getTarefasFiltardas()" />
    </div>
</template>
