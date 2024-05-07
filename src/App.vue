<script setup>
import { reactive } from 'vue';


  const state = reactive({
    filter: 'all',
    tempTask: '',
    tasks: [
      {
        name: 'Estudar ES6',
        done: false,
      },
      {
        name: 'Estudar SASS',
        done: false,
      },
      {
        name: 'Ir para academia',
        done: true,
      }
    ]
  });

  const getToDoTasks = () => {
    return state.tasks.filter(task => !task.done)
  };
  
  const getDoneTasks = () => {
    return state.tasks.filter(task => task.done)
  };

  const getFilterdTasks = () => {
    const {filter} = state;
     
    switch(filter){
      case 'to-do':
        return getToDoTasks();
        break;
      
      case 'done':
        return getDoneTasks();
        break;

      default:
        return state.tasks;
    }
  };

  const submitTak = () => {
    const newTask = {
      name: state.tempTask,
      done: false,
    };

    state.tasks.push(newTask);
    state.tempTask = '';
  }

</script>
 
<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getToDoTasks().length }} tarefas pendentes
      </p>
    </header>

    <form @submit.prevent="submitTak">
    <div class="row">
      <div class="col">
        <input :value="state.tempTask" @change="e => state.tempTask = e.target.value" required type="text" placeholder="Descrição da tarefa" class="form-control">
      </div>
      <div class="col-md-1">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
    </div>

    <div class="col-md-2">
      <select @change="e => state.filter = e.target.value" class="form-control">
        <option value="all">Todas as tarefas</option>
        <option value="to-do">Pendentes</option>
        <option value="done">Finalizadas</option>
      </select>
    </div>
  </form>

  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="task in getFilterdTasks()">
      <input @change="e => task.done = e.target.checked" :checked="task.done" :id="task.name" type="checkbox">
      <label :class="{ done: task.done}" class="ms-3" :for="task.name">
        {{ task.name }}
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
