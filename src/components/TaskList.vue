<script setup>

    const props = defineProps(['tasks']);

    console.log(props.tasks);
</script>


<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="task in props.tasks" :key="task.name">
        <input @change="e => task.done = e.target.checked" :checked="task.done" :id="task.name" type="checkbox">
        <label :class="{ done: task.done}" class="ms-3" :for="task.name">
            {{ task.name }}
        </label>
        </li>
    </ul>
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>