<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaDeTarefa from './components/ListaDeTarefa.vue'

const estado = reactive({
  filtro:"todos",
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizado: false,
    },
    {
      titulo: "Estudar Sass",
      finalizada: false,
    },
    {
      titulo: "Ir para academia",
      finalizada: true,
    },
  ]
})

const getTarefasPendentes = () => {
  estado.tarefas.filter(tarefa => !tarefa.finalizada )
}

const getTarefasFinalizada = () => {
  estado.tarefas.filter(tarefa => tarefa.finalizada )
}
const getTarefasFiltradas = () => {
  const filtro = estado.filtro;

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case "finalizadas":
      return getTarefasFinalizada();
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
  estado.tarefaTemp = "";
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :troca-filtros="evento => estado.filtro = estado.filtro.values" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <ListaDeTarefa :tarefas="getTarefasFiltradas()"/>
  </div>
</template>
<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
