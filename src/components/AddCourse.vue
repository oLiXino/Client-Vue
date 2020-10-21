<template>
  <div>
    <form @submit.prevent="addCourse">
        <input type="text" v-model="code" name="code" placeholder="Course Code">
        <input type="text" v-model="name" name="name" placeholder="Course Name">
        <input type="submit" value="Add Course" class="btn">
    </form>
  </div>
</template>

<script>

export default {
  name: "AddCourse",
  data() {
    return {
      code: '',
      name: ''
    }
  },
  methods: {
    addCourse(e) {
      e.preventDefault();
      const newCourse = {
        id: this.code,
        name: this.name
      }
      this.$emit('add-course', newCourse);
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