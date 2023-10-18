<script setup>
    const props = defineProps(['tarefasPendentes']);
</script>
<template>
     <header class="p-5 mb-4 mt-4 bg-ligth roudend-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ props.tarefasPendentes }} tarefas pendente
      </p>
    </header>
</template>