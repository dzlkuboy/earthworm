<template>
  <div class="relative w-full flex flex-col">
    <h2 class="my-4 text-3xl text-blue-500">English Course</h2>
    <div class="h-full overflow-y-auto scrollbar-hide">
      <div
        v-if="courses.length"
        class="h-[79vh] flex flex-wrap p-1 pb-96 gap-8 overflow-y-auto justify-start"
      >
        <template v-for="course in courses" :key="course.id">
          <NuxtLink :href="`/main/${course.id}`">
            <CourseCard :title="course.title" />
          </NuxtLink>
        </template>
      </div>
      <Loading v-else />
    </div>
  </div>
</template>

<script setup lang="ts">
import { type Course } from "~/store/course";
import { fetchCourses } from "~/api/course";
import Loading from "~/components/Loading.vue";
import CourseCard from "~/components/courses/CourseCard.vue";
import { ref, onMounted } from "vue";

const courses = ref<Course[]>([]);

onMounted(async () => {
  courses.value = await fetchCourses();
});
</script>
