<script>
export default {
  name: "Header",
  props: {
    title: String,
  },
};
</script>

<template>
  <h2>{{ title }}</h2>
</template>

<style scoped>
h2 {
  font-weight: 700;
}
</style>
