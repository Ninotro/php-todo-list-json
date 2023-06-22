<script>
import axios from "axios";

export default {
  data() {
    return {
      tasks: [],
      newTask: {
        titolo: "",
        
      }
    };
  },
  methods: {
    onSubmit() {
      const url = "http://localhost/php-todo-list-json/php/postStudent.php";
      const data = this.newTask;
      console.log(this.newTask);
      const headers = {
        headers: { "Content-Type": "multipart/form-data" }
      };

      axios
        .post(url, data, headers)
        .then(response => {
          this.tasks = response.data;
          this.newTask.titolo = "";
          
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
        {{ task.titolo }} 
      </li>
    </ul>
    <form @submit.prevent="onSubmit">
      <label for="title">Cose da fare</label>
      <input type="text" name="titolo" id="titolo" v-model="newTask.titolo" />
      <br />
      
      <input type="submit" value="Add Task" />
    </form>
  </div>
</template>

<style>
</style>