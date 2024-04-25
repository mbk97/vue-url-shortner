<template>
  <div class="about-container">
    <img :src="imagePath" alt="hello" class="img" />
    <p>The simplest URL shortner you were waiting for</p>
  </div>
</template>
<script>
import image from "../assets/logo_h.png";
export default {
  name: "About",
  data() {
    return {
      imagePath: image,
    };
  },
};
</script>
<style scoped>
.about-container {
  font-family: "Roboto", sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.img {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 30px;
}

p {
  text-align: center;
}
</style>
