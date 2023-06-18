<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')" :class="{ active: current == 'all' }">
      View All
    </button>
    <button
      @click="updateFilter('complete')"
      :class="{ active: current == 'complete' }"
    >
      Completed
    </button>
    <button
      @click="updateFilter('process')"
      :class="{ active: current == 'process' }"
    >
      Process
    </button>
  </nav>
</template>

<script>
export default {
  props: ["current"],
  data() {
    return {};
  },
  methods: {
    updateFilter(by) {
      this.$emit("updateProject", by);
    },
  },
};
</script>

<style scoped>
.filter-nav button {
  background: none;
  border: none;
  color: wheat;
  outline: none;
  font-size: 16px;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1;
  font-weight: bold;
  cursor: pointer;
  padding: 5px;
}
.filter-nav button:hover {
  color: floralwhite;
}
.filter-nav button.active{
	color: brown;
}
</style>