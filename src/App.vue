<script>
import TodoCard from './components/TodoCard.vue';
import TodoForm from './components/TodoForm.vue';

export default {
  components: {
    TodoCard,
    TodoForm,
  },
  data() {
    return {
      tasks: [
        {
          title: "用 AXIOS 串接API",
          content: "將任務改成若可以連接得到伺服端，則使用伺服端資料修改。"
        },
        {
          title: "實作 Flask RESTful API",
          content: "用 Flask 實作 CRUD"
        },
        {
          title: "完成 Vue.js 前端頁面",
          content: "基本 TODO LIST 頁面"
        },

      ],
    }
  },
  computed: {

  },
  methods: {
    addTask(title, content) {
      const task = { title: title, content: content };
      this.tasks.unshift(task);
    },
    deleteTask(index) {
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
