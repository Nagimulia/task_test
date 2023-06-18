<template>
  <div class="home">
    <FilterProject @updateProject="current = $event" :current="current" />
    <div v-for="project in sortProject" :key="project.id">
      <SingleProject
        :project="project"
        @deleteProject="handleProject"
        @updateCompleted="handleCompleted"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SingleProject from "@/components/SingleProject.vue";
import FilterProject from "@/components/FilterProject.vue";

export default {
  name: "HomeView",
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  components: {
    SingleProject,
    FilterProject,
  },
  async mounted() {
    let responce = await axios.get("http://localhost:3000/projects");
    this.projects = responce.data;
  },
  methods: {
    handleProject(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    handleCompleted(id) {
      let findProject = this.projects.find((project) => project.id == id);
      findProject.completed = !findProject.completed;
    },
  },
  computed: {
    sortProject() {
      if (this.current === "all") {
        return this.projects;
      }
      if (this.current === "complete") {
        return this.projects.filter((project) => project.completed == true);
      }
      if (this.current === "process") {
        return this.projects.filter((project) => project.completed == false);
      }
    },
  },
};
</script>

