<script setup>
import { reactive } from 'vue';
import CabecalhoPrincipal from './components/CabecalhoPrincipal.vue'
import FormularioPrincipal from './components/FormularioPrincipal.vue'
import ListaDeTarefa from './components/ListaDeTarefas.vue'

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
    <CabecalhoPrincipal :tarefas-pendentes="getTarefasPendentes().length" />
    <FormularioPrincipal :troca-filtros="evento => estado.filtro = estado.filtro.values" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <ListaDeTarefa :tarefas="getTarefasFiltradas()"/>
  </div>
</template> 
<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
