<template>
  <form @submit.prevent="handleSubmit">
    <label> Title: </label>
    <input type="text" v-model="title" />
    <label>Deadline</label>
    <textarea required v-model="deadline"></textarea>
    <button>Add New Project</button>
  </form>
</template>


<script>
import axios from "axios";

export default {
  data() {
    return {
      title: "",
      deadline: "",
      url: "http://localhost:3000/projects/",
    };
  },
  methods: {
    async handleSubmit() {
      await axios.post(this.url, {
         title: this.title,
        deadline: this.deadline,
        completed: false,
      });
      this.$router.push({name:'home'})
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