<template>
    <div>
        <div v-bind:key="course.id" v-for="course in courses">
            <Course v-bind:course="course" 
            v-on:del-course="$emit('del-course', course.id)"/>
        </div>
    </div>
</template>

<script>
import Course from './Course'

export default {
    name: "Courses",
    components: {
        Course
    },
    props: ["courses"]
}
</script>

<style scoped>

</style>