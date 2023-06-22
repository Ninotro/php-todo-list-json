<script >

import axios from 'axios';

export default {
  data() {

    return {
      students: [],

      newStudent: {
        name: "",
        last_name: ""
      }
    };
  },
  methods: {
    onSubmit() {

      const url = 'http://localhost/php-todo-list-json/php/index.php';
      const data = this.newStudent;
      const headers = {
          headers: { 'Content-Type': 'multipart/form-data' } 
      };

      axios.post(url, data, headers)
           .then(response => {
          
            this.students = response.data;
          
            this.newStudent.name = "";
            this.newStudent.last_name = "";

          })
           .catch(error => console.error("error", error));
    }
  },
  mounted() {
    
    axios.get('http://localhost/php-todo-list-json/php/index.php')
         .then(response => {
            this.students = response.data;
         });
  }
};
</script>

<template>
    
  <div>
    <h1>Studenti</h1>
    <ul>
      <li
        v-for="(student, index) in students"
        :key="index"
      >
      {{ student.name }} {{ student.last_name }}
    </li>
    </ul>
    <form @submit.prevent="onSubmit">
      <label for="name">Name </label>
      <input type="text" name="name" id="name" v-model="newStudent.name">
      <br />
      <label for="last_name">Last name </label>
      <input type="text" name="last_name" id="last_name" v-model="newStudent.last_name">
      <br />
      <input type="submit" value="CREATE NEW STUDENT">
    </form>
  </div>
</template>


<style >

</style>
