<template>
  <div class="center">
    <div class="title">Simon</div>
    <div class="switches">
      <input type="checkbox" class="toggle" id="on" @change="powerCheckBox" />
      <button class="button" id="start" @click="startButtonClick">Start</button>
    </div>
    <div class="text1">
      <span> POWER</span>
    </div>
    <div id="turn">{{ counter }}</div>
    <div class="text2">COUNT</div>
  </div>
</template>

<script>
export default {
  props: ["counter", "powerCheckBox", "startButtonClick"],
};
</script>

<style scoped>
.center {
  position: absolute;
  background: grey;
  border-radius: 50%;
  height: 250px;
  width: 250px;
  border: 10px solid black;
  top: 50%;
  left: 50%;
  margin: -125px 0px 0px -125px;
}
.toggle {
  margin-left: 20px;
  margin-right: 20px;
  width: 20px;
  height: 20px;
}

.button {
  border-radius: 50%;
  font-size: 1.5em;
  background-color: lightgray;
  width: 75px;
}
.switches {
  position: absolute;
  font-family: "Original Surfer", cursive;
  margin-left: 15px;
  margin-top: 110px;
}

.text2 {
  position: absolute;
  font-family: "Original Surfer", cursive;
  margin-left: 83px;
  margin-top: 205px;
}

.text1 {
  position: absolute;
  font-family: "Original Surfer", cursive;
  margin-left: 20px;
  margin-top: 142px;
}

.title {
  font-family: "Original Surfer", cursive;
  position: absolute;
  font-size: 40px;
  margin-left: 50px;
  margin-top: 40px;
}
#turn {
  position: absolute;
  background: #330000;
  color: red;
  font-family: courier;
  font-size: 20px;
  height: 30px;
  width: 50px;
  margin-left: 90px;
  margin-top: 170px;
  text-align: center;
  vertical-align: middle;
  line-height: 30px;
}
@media (max-width: 1200px) {
  .center {
    left: 30%;
  }
}
</style>
