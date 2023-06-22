<script>
import axios from "axios";

export default {
  data() {
    return {
      tasks: [],
      newTask: {
        titolo: "",
        descrizione: ""
      }
    };
  },
  methods: {
    onSubmit() {
      const url = "http://localhost/php-todo-list-json/php/index.php";
      const data = this.newTask;
      const headers = {
        headers: { "Content-Type": "multipart/form-data" }
      };

      axios
        .post(url, data, headers)
        .then(response => {
          this.tasks = response.data;
          this.newTask.titolo = "";
          this.newTask.descrizione = "";
        })
        .catch(error => console.error("Errore nella richiesta POST", error));
    }
  },
  mounted() {
    axios
      .get("http://localhost/php-todo-list-json/php/index.php")
      .then(response => {
        this.tasks = response.data;
      })
      .catch(error => console.error("Errore nella richiesta GET", error));
  }
};
</script>


<template>
  <div>
    <h1>To-Do List</h1>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        {{ task.title }} - {{ task.description }}
      </li>
    </ul>
    <form @submit.prevent="onSubmit">
      <label for="title">Title</label>
      <input type="text" name="titolo" id="titolo" v-model="newTask.titolo" />
      <br />
      <label for="description">Description</label>
      <input
        type="text"
        name="descrizione"
        id="descrizione"
        v-model="newTask.descrizione"
      />
      <br />
      <input type="submit" value="Add Task" />
    </form>
  </div>
</template>

<style></style>