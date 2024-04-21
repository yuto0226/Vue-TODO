<script>
import { ref } from 'vue';
import TodoCard from './components/TodoCard.vue';
import TodoForm from './components/TodoForm.vue';

import axios from 'axios';


export default {
  setup() {
    const tasks = ref([]);
    const apiIsConnected = ref(true);
    axios.get('http://localhost:5000/api/task/')
      .then((res) => {
        console.log(res.data);
        tasks.value = res.data;
        apiIsConnected.value = true;
        console.log(apiIsConnected);
      }).catch((error) => {
        console.log(error);
        tasks.value = [
          {
            id: "01",
            title: "用 AXIOS 串接API",
            content: "將任務改成若可以連接得到伺服端，則使用伺服端資料修改。"
          },
          {
            id: "02",
            title: "實作 Flask RESTful API",
            content: "用 Flask 實作 CRUD"
          },
          {
            id: "03",
            title: "完成 Vue.js 前端頁面",
            content: "基本 TODO LIST 頁面"
          },
        ];
        apiIsConnected.value = false;
      });
    return { tasks, apiIsConnected };
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
          this.apiIsConnected.value = true;
          console.log(response);
        })
        .catch(function (error) {
          this.apiIsConnected.value = false;
          console.log(error);
        });
      this.tasks.unshift(task);
    },
    deleteTask(index) {
      axios.delete('http://localhost:5000/api/task/' + index + '/')
        .then(function (response) {
          this.apiIsConnected.value = true;
          console.log(response);
        })
        .catch(function (error) {
          this.apiIsConnected.value = false;
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
    <p v-if="apiIsConnected.valueOf()">API 連接成功</p>
    <p v-else>API 連接失敗</p>
    <TodoForm :tasks="tasks" @newTask="addTask"></TodoForm>
    <div v-for="({ id, title, content }, index) in tasks" :key="index">
      <TodoCard :id="id" :title="title" :content="content" @deleteTask="deleteTask(index)"></TodoCard>
    </div>


  </main>
</template>

<style scoped></style>
