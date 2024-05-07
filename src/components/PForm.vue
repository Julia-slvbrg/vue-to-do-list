<script setup>
    const props = defineProps(['submitTask', 'tempTask', 'changeFilter', 'editTempTask'])
</script>

<template>
    <form @submit.prevent="props.submitTask">
    <div class="row">
      <div class="col">
        <input :value="props.tempTask" @change="props.editTempTask" required type="text" placeholder="Descrição da tarefa" class="form-control">
      </div>
      <div class="col-md-1">
        <button type="submit" class="btn btn-primary btn-md">Cadastrar</button>
      </div>
    </div>

    <div class="col-md-2">
      <select @change="props.changeFilter" class="form-control">
        <option value="all">Todas as tarefas</option>
        <option value="to-do">Pendentes</option>
        <option value="done">Finalizadas</option>
      </select>
    </div>
  </form>
</template>