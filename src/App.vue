<script>
import { onMounted, onUpdated, ref } from 'vue';
import TodoCard from './components/TodoCard.vue';
import TodoForm from './components/TodoForm.vue';

import axios from 'axios';


export default {
  setup() {
    const tasks = ref([]);
    axios.get('http://localhost:5000/api/task/')
      .then((res) => {
        console.log(res.data);
        tasks.value = res.data;
      }).catch((error) => {
        console.log(error);
      });
    return { tasks };
  },
  components: {
    TodoCard,
    TodoForm,
  },
  data() {
    return {

    }
  },
  computed: {

  },
  methods: {
    addTask(title, content) {
      const task = { title: title, content: content };
      axios.post('http://localhost:5000/api/task/', {
        title: title,
        content: content
      })
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });
      this.tasks.unshift(task);
    },
    deleteTask(index) {
      axios.delete('http://localhost:5000/api/task/' + index + '/')
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });
      this.tasks.splice(index, 1);
    }
  }
}
</script>

<template>
  <main class="">
    <h2>TODO</h2>
    <hr>
    <TodoForm :tasks="tasks" @newTask="addTask"></TodoForm>
    <div v-for="({ title, content }, index) in tasks" :key="index">
      <TodoCard :title="title" :content="content" @deleteTask="deleteTask(index)"></TodoCard>
    </div>


  </main>
</template>

<style scoped></style>
