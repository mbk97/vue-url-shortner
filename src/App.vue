<script>
import Header from "./Components/Header.vue";
import About from "./Components/About.vue";
import Input from "./Components/Input.vue";
export default {
  components: {
    Header,
    About,
    Input,
  },
};
</script>

<template>
  <div class="container">
    <div class="header_wrapper">
      <Header title="Short it" />
      <About />
      <Input />
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
}

.header_wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: auto;
  height: 300px;
  justify-content: space-between;
  margin-top: 50px;
}
</style>
