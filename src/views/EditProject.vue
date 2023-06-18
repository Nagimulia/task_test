<template>
  <form @submit.prevent="handleEdit">
    <label> Title: </label>
    <input type="text" v-model="title" />
    <label>Deadline</label>
    <textarea required v-model="deadline"></textarea>
    <button>Edit Project</button>
  </form>
</template>

<script>
import axios from "axios";

export default {
  props: ["id"],
  data() {
    return {
      title: "",
      deadline: "",
    };
  },

  async mounted() {
    let { data } = await axios.get("http://localhost:3000/projects/" + this.id);
    this.title = data.title;
    this.deadline = data.deadline;
  },
  methods: {
    async handleEdit() {
      await axios.patch(`http://localhost:3000/projects/${this.id}`, {
        title: this.title,
        deadline: this.deadline,
      });
      this.$router.push('/');
    },
  },
};
</script>

<style scoped>
form {
  background: wheat;
  padding: 20px;
  border-radius: 10px;
  margin-top: 60px;
}
label {
  display: block;
  color: blueviolet;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1;
  margin: 20px 0 10px 0;
}
input {
  padding: 10px;
  border: 0;
  border-bottom: 1px solid wheat;
  width: 100%;
  box-sizing: border-box;
}
textarea {
  border: 1px solid wheat;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  height: 100px;
}

form button {
  display: block;
  margin: 20px auto 0;
  background: blueviolet;
  color: aliceblue;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}
</style>