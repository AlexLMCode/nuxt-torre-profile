<template>
  <button class="button">{{ skillName }}</button>
</template>

<script>
export default {
  props: {
    skillName: {
      type: String,
      required: true,
    },
  },
}
</script>

<style scoped>
.button {
  background-color: #444141;
  border-radius: 30px;
  /* color: #fff; */
  cursor: pointer;
  padding: 5px 25px;
  font-size: 12px;
  /* font-weight: bold; */
  /* letter-spacing: 1px; */
  border: none;
  margin: 0.4rem;
}
</style>