<!-- src/components/ButtonPanel.vue -->
<template>
  <div class="button-layout">
    <div class="button-row">
      <button class="arcade-btn"></button>
      <button class="arcade-btn"></button>
      <button class="arcade-btn"></button>
    </div>
    <div class="button-row">
      <button class="arcade-btn"></button>
      <button class="arcade-btn"></button>
      <button class="arcade-btn"></button>
    </div>
  </div>
</template>

<style scoped>
.button-layout {
  display: flex;
  flex-direction: column;
  gap: 20px;
  padding: 10px;
  /* Perspective horizontale */
  perspective: 400px;
}

.button-row {
  display: flex;
  gap: 20px;
  justify-content: center;
}

.arcade-btn {
  width: 54px;
  height: 38px;
  border-radius: 50% / 40%;
  border: none;
  background: radial-gradient(ellipse at 60% 30%, #ffe066 40%, #ff6a00 80%, #ff2d55 100%);
  box-shadow: 
    0 4px 16px #ff2d5555,
    0 0 0 2px #ffe066,
    0 0 0 5px #2d004d,
    inset 0 2px 8px #fff8,
    inset 0 -8px 16px #ff6a00cc;
  cursor: pointer;
  transform: rotateX(25deg);
  transition: 
    transform 0.1s,
    box-shadow 0.1s;
  position: relative;
}

.arcade-btn:active {
  transform: rotateX(25deg) scale(0.95) translateY(2px);
  box-shadow: 
    0 2px 8px #ff2d55aa,
    0 0 0 2px #ffe066,
    0 0 0 5px #ff6a00,
    inset 0 1px 4px #fff6,
    inset 0 -6px 12px #ff6a00cc;
}
</style>
