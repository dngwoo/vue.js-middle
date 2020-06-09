<template>
  <div class="clearAllContainer shadow" @click="clearTodo">
    <span class="clearAllBtn">Clear All</span>
  </div>
</template>

<script>
export default {
  methods: {
    clearTodo() {
      this.$emit("clearAll");
    }
  }
};
</script>

<style scoped>
.clearAllContainer {
  width: 8.5rem;
  height: 50px;
  line-height: 50px;
  background: white;
  border-radius: 5px;
  margin: 0 auto;
}
.clearAllBtn {
  color: #e20303;
  display: block;
  cursor: pointer;
}
.clearAllContainer:active {
  transform: scale(0.9);
}
</style>