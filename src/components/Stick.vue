<!-- src/components/Stick.vue -->
<template>
  <div class="stick-wrapper">
    <div class="base"></div>
    <div class="stick"></div>
    <div class="ball"></div>
  </div>
</template>

<style scoped>
.stick-wrapper {
  position: relative;
  width: 60px;
  height: 100px;
  margin: 0 20px;
}

.base {
  position: absolute;
  bottom: 0;
  width: 60px;
  height: 20px;
  background: #444;
  border-radius: 10px;
  box-shadow: inset 0 0 5px #000;
}

.stick {
  position: absolute;
  bottom: 14px;
  left: 28px;
  width: 4px;
  height: 64px;
  background: #666;
  transform-origin: bottom center;
  transition: transform 0.2s;
}

.ball {
  position: absolute;
  bottom: 78px;
  left: 20px;
  width: 20px;
  height: 20px;
  background: red;
  border-radius: 50%;
  box-shadow: 0 0 5px red;
}
</style>
