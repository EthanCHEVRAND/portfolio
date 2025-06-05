<!-- src/components/Stick.vue -->
<template>
  <div class="stick-arcade">
    <div class="stick-ellipse"></div>
    <div class="stick-bar"></div>
    <div class="stick-ball"></div>
  </div>
</template>

<style scoped>
.stick-arcade {
  position: relative;
  width: 120px;
  height: 100px;
  display: flex;
  align-items: flex-end;
  justify-content: center;
}

.stick-ellipse {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 100px;
  height: 32px;
  background: radial-gradient(ellipse at center, #2d004d 60%, #1a0033 100%);
  border: 3px solid #ff6a00;
  border-radius: 50% / 50%;
  box-shadow: 0 4px 16px #ff2d5555, 0 0 0 2px #ffe066;
  z-index: 1;
}

.stick-bar {
  position: absolute;
  bottom: 16px;
  left: 50%;
  transform: translateX(-50%);
  width: 12px;
  height: 48px;
  background: linear-gradient(90deg, #ff2d55 0%, #ff6a00 100%);
  border-radius: 6px;
  z-index: 2;
  box-shadow: 0 0 8px #ff6a00aa;
}

.stick-ball {
  position: absolute;
  bottom: 56px;
  left: 50%;
  transform: translateX(-50%);
  width: 32px;
  height: 32px;
  background: radial-gradient(circle at 30% 30%, #ffe066 60%, #ff6a00 100%);
  border-radius: 50%;
  border: 3px solid #ff6a00;
  box-shadow: 0 0 12px #ff2d55aa, 0 0 0 2px #ffe066;
  z-index: 3;
}
</style>
