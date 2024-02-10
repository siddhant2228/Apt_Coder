<script setup>
import { reactive } from 'vue';
import Header from './components/Header.vue';
import Form from './components/Form.vue';
import TaskList from './components/TaskList.vue';

const state = reactive({
  filter: 'all',
  tempTask: '',
  tasks: [
    {
      title: 'Study ES6',
      completed: false,
    },
    {
      title: 'Study SASS',
      completed: false,
    },
    {
      title: 'Go to the gym',
      completed: true,
    }
  ]
});

const getPendingTasks = () => {
  return state.tasks.filter(task => !task.completed);
};

const getCompletedTasks = () => {
  return state.tasks.filter(task => task.completed);
};

const getFilteredTasks = () => {
  const { filter } = state;
  switch (filter) {
    case 'pending':
      return getPendingTasks();
    case 'completed':
      return getCompletedTasks();
    default:
      return state.tasks;
  }
};

const addTask = () => {
  const newTask = {
    title: state.tempTask,
    completed: false,
  };
  state.tasks.push(newTask);
  state.tempTask = '';
};
</script>

<template>
<div class="container">
  <Header :pending-tasks="getPendingTasks().length" />
  <Form :change-filter="event => state.filter = event.target.value" :temp-task="state.tempTask" :edit-temp-task="event => state.tempTask = event.target.value" :add-task="addTask" />
  <TaskList :tasks="getFilteredTasks()" />
</div>
</template>
