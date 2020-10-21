<template>
  <div>
    <form @submit.prevent="modifyCourse">
        <input type="text" v-model="code" name="code" placeholder="Course Code">
        <input type="text" v-model="name" name="name" placeholder="New Course Name">
        <input type="submit" value="Edit Course" class="btn">
    </form>
  </div>
</template>

<script>

export default {
  name: "EditCourse",
  data() {
    return {
      code: '',
      name: ''
    }
  },
  methods: {
    modifyCourse(e) {
      e.preventDefault();
      const editCourse = {
        id: this.code,
        name: this.name
      }
      this.$emit('modify-course', editCourse);
      this.code = '';
      this.name = '';
    }
  }
}
</script>

<style scoped>
  form {
    display: flex;
  }
  input[type="text"] {
    flex: 10;
    padding: 5px;
  }
  input[type="submit"] {
    flex: 2;
  }
</style>