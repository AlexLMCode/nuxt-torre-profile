<template>
  <div class="hex">
    <img :src="img" alt="some" />
  </div>
</template>

<script>
export default {
  props: {
    img: {
      type: String,
      required: true,
    },
  },
}
</script>


<style scoped>
img {
  width: 100%;
  height: auto;
  display: block;
  object-fit: cover;
}

.hex {
  display: flex;
  position: relative;
  width: 200px;
  height: 220px;
  background-color: #424242;
  -webkit-clip-path: polygon(
    50% 0%,
    100% 25%,
    100% 75%,
    50% 100%,
    0% 75%,
    0% 25%
  );
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
}
</style>