<script setup>
  import { reactive } from 'vue';
  import PHeader from './components/PHeader.vue'
  import PForm from './components/PForm.vue'
  import TaskList from './components/TaskList.vue'


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

  const getFilteredTasks = () => {
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

  const submitTask = () => {
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
    <PHeader :toDoTasks="getToDoTasks().length"/>
    <PForm 
      :tempTask="state.tempTask" 
      :editTempTask="(e) => state.tempTask = e.target.value" 
      :submitTask="submitTask"
      :changeFilter="(e) => state.filter = e.target.value"
    />
    <TaskList 
      :tasks="getFilteredTasks()"
    />  
  </div>
</template>