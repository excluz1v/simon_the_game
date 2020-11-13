<template>
  <div @click="pickingColor"></div>
</template>

<script>
export default {
  props: ["color", "pickingColor"],
};
</script>

<style scoped>
div {
  position: absolute;
  width: 250px;
  height: 250px;
  top: 50%;
  left: 50%;
  border: 5px solid black;
}
@media (max-width: 1200px) {
  div {
    left: 30%;
  }
}
</style>
