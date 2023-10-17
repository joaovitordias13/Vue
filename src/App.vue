<script setup>
import { reactive } from 'vue';
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
    <header class="p-5 mb-4 mt-4 bg-ligth roudend-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendente
      </p>
    </header>
    <form @submit="cadastraTarefa">
    <div class="row">
      <div class="col">
        <input @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
      </div>
      <div class="col-md-1">
        <button type="submit" class="btn btn-primary">
          Cadastrar
        </button>
      </div>
      <div class="col-md-2">
        <select @change="evento => estado.filtro = evento.target" class="form-control">
          <option value="todas">Todas tarefas</option>
          <option value="todas">Tarefas Pendentes</option>
          <option value="todas">Tarefas Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for-key="tarefa in getTarefasFiltradas()">
      <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
      <label :class="{done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
  </div>
</template>
<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
