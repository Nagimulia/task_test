<template>
  <div class="project" :class="{ activeCompleted: project.completed }">
    <div class="actions">
      <h3 @click="showHideDeadlineMethod">
        {{ project.title }}
      </h3>
      <div class="icons">
        <span class="material-icons" @click="completeMethod">done</span>
        <span class="material-icons" @click="deleteProject">delete</span>
        <router-link :to="{ name: 'editProject', params: { id: project.id } }">
          <span class="material-icons">edit</span>
        </router-link>
      </div>
    </div>
    <div class="deadline" v-if="showDeadline">
      <p>
        {{ project.deadline }}
      </p>
    </div>
  </div>
</template>


<script>
import axios from "axios";

export default {
  props: ["project"],
  data() {
    return {
      showDeadline: false,
      url: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  methods: {
    showHideDeadlineMethod() {
      this.showDeadline = !this.showDeadline;
    },
    async deleteProject() {
      await axios.delete(this.url);
      this.$emit("deleteProject", this.project.id);
    },
    async completeMethod() {
      await axios.patch(this.url, {
        completed: !this.project.completed,
      });
      this.$emit("updateCompleted", this.project.id);
    },
  },
};
</script>

<style scoped>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 10px solid red;
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}
.material-icons:hover {
  color: #777;
}
.activeCompleted {
  border-left: 10px solid green;
}
</style>