<template>
  <div id="app" class="container">
    <h1 id="header">👨🏽‍💻Students 👩🏻‍💻</h1>

    <student :students="students" @delete:student="deleteStudent"/>
    <student-form @add:student="addStudent"/>
  </div>
</template>

<script>
import student from "./components/students";
import studentForm from "./components/studentForm";

export default {
  name: "app",
  components: {
    student,
    studentForm
  },
  data() {
    return {
      students: []
    };
  },
  mounted() {
    this.getStudents();
  },
  methods: {
    async getStudents() {
      try {
        const response = await fetch("http://localhost:3000/students");
        const data = await response.json();
        this.students = data;
      } catch (error) {
        console.error(error);
      }
    },
    async addStudent(student) {
      try {
        const response = await fetch("http://localhost:3000/students", {
          method: "POST",
          body: JSON.stringify(student),
          headers: { "Content-type": "application/json; charset=UTF-8" }
        });
        const data = await response.json();
        this.students = [...this.students, data];
      } catch (error) {
        console.error(error);
      }
    },
    async deleteStudent(id) {
      try {
        let answer = confirm(
          "Are you sure, this user will be removed forever ☠️? , press cancel if you don't want to Delete"
        );
        if (answer) {
          await fetch(`http://localhost:3000/students/` + id, {
            method: "DELETE"
          }).then(() => this.getStudents());
        }
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
}
#app {
  font-family: "PT-Sans", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #43534d;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
}

#header{
  color: #008a17;
  font-size: 50px;
}

button {
  background: #009435;
  border: 1px solid #009435;
}
</style>
