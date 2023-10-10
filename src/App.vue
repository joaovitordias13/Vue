<script setup>
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-ligth roudend-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui 4 tarefas pendente
      </p>
    </header>
    <form >
    <div class="row">
      <div class="col">
        <input type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
      </div>
      <div class="col-md-1">
        <button type="submit" class="btn btn-primary">
          Cadastrar
        </button>
      </div>
      <div class="col-md-2">
        <select class="form-control">
          <option value="todas">Todas tarefas</option>
          <option value="todas">Tarefas Pendentes</option>
          <option value="todas">Tarefas Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
  </div>

</template>


<style scoped>
</style>
