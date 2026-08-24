<script setup>
import { reactive } from 'vue';
import cabecalho from './components/cabecalho.vue';
import formulario from './components/formulario.vue';
import listaDeTarefas from './components/listaDeTarefas.vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [// abrindo o array
    {
      titulo: 'Estudar ES6',
      finalizado: false,
    },
    {
      titulo: 'Estudar SASS',
      finalizado: false,
    },
    {
      titulo: 'Ir para  a academia',
      finalizada: true,
    }
  ]
})

//funcões
const getTarefasPendentes = () => { //ativando o arrow function e usando o filter,para encontrar os objetos
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => { //ativando o arrow function e usando o filter,para encontrar os objetos
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';//para deixar o campo sempre vazio
}
</script>

<template>
  <div class="container">
    <cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <formulario :trocar-filtro="evento => estado.filtro = evento.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <listaDeTarefas :tarefas="getTarefasFiltradas()" />
  </div>
</template>


