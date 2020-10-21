<template>
    <div class="course">
        <p>
        <span class="code">{{course.id}}</span>
        <span>{{course.name}}</span>
        <button @click="$emit('del-course', course.id)" class="btn">x</button>
        </p>
    </div>
</template>

<script>
export default {
    name: "Course",
    props: ["course"],
    components: {
    }
}
</script>

<style scoped>
  .course {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
  }
  .code {
    margin-right: 10em;
  }
  .is-complete {
    text-decoration: line-through;
  }
  .btn {
    background: #54C187;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
    margin-left: 10px;
  }

</style>