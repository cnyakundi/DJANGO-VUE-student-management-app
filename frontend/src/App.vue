<template>
  <div id="app">

   <div class="container">
      <form v-on:submit.prevent="createStudent">
      <div class="form-group row">
        <input type="text" class="form-control col-3 mx-2" placeholder="Name" v-model="student.name">
        <input type="text" class="form-control col-3 mx-2" placeholder="Course" v-model="student.course">
        <input type="text" class="form-control col-3 mx-2" placeholder="Rating" v-model="student.rating">
       <button class="btn btn-success"> Submit</button>
      </div>
    </form>
   </div>

<table class="table">
  <thead>
    <th>Name</th>
    <th>Course</th>
    <th>Rating</th>
  </thead>
  <tbody>
    <tr v-for="student in students" :key="student.id">
      <td> {{ student.name }} </td>
      <td> {{ student.course }} </td>
      <td>{{ student.rating }} </td>
    </tr>
  </tbody>
</table>
</div>
</template>

<script>
export default {
  name: 'App',
data(){
    return {
      student: {
        'name':'',
        'course': '',
        'rating': '',
      },
      students: []
    }
},

  async created() {

    const response = await fetch('http://127.0.0.1:8000/api/students/');

    this.students= await response.json()
  },

methods: {
      async createStudent(){
       var response = await fetch('http://127.0.0.1:8000/api/students/', {
         method: 'post',
         headers: {'Content-Type': 'application/json'},
         body: JSON.stringify(this.student)
       });
        this.students.push(await response.json())
  }


},


}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
