<template>
  <div id="app">
    <Header />
    <Separator />
    <AddCourse v-on:add-course="addCourse"/>
    <Separator />
    <EditCourse v-on:modify-course="modifyCourse"/>
    <Separator />
    <Courses v-bind:courses="courses" v-on:del-course="deleteCourse"/>
  </div>
</template>

<script>
import Header from './components/layout/Header'
import Separator from './components/Separator'
import Courses from './components/Courses'
import AddCourse from './components/AddCourse'
import EditCourse from './components/EditCourse'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Header,
    Separator,
    Courses,
    AddCourse,
    EditCourse
  },
  data() {
    return {
      courses: []
    }
  },
  methods: {
    addCourse(newCourse) {
      const {id, name} = newCourse;
      axios.post('https://vie8z9f1q4.execute-api.us-east-1.amazonaws.com/dev/api/courses',{
        id: id,
        name: name
      })
      .then(res => this.courses = [...this.courses, res.data])
      .catch(err => console.log(err));
    },
    deleteCourse(id) {
      axios.delete(`https://vie8z9f1q4.execute-api.us-east-1.amazonaws.com/dev/api/courses/${id}`)
      .then(res => this.courses = this.courses.filter(course => course.id != res.data.id)) 
      .catch(err => console.log(err)); 
    },
    modifyCourse(editCourse) {
      const {id, name} = editCourse;
      let course = this.courses.find(course => course.id.localeCompare(id) == 0);
      axios.put(`https://vie8z9f1q4.execute-api.us-east-1.amazonaws.com/dev/api/courses/${id}`,{
        name: name
      })
      .then(res => course.name = res.data.name)
      .catch(err => console.log(err));
    }
  },
  created() {
    axios.get('https://vie8z9f1q4.execute-api.us-east-1.amazonaws.com/dev/api/courses')
    .then(res => this.courses = res.data)
    .catch(err => console.log(err));
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
    padding: 10px;
  }
  .btn {
    display: inline-block;
    border: none;
    background: #6A63CB;
    color: white;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #554FAA;
  }
</style>
