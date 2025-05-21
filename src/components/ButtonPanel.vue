<!-- src/components/ButtonPanel.vue -->
<template>
  <div class="buttons">
    <button class="arcade-button red"></button>
    <button class="arcade-button blue"></button>
    <button class="arcade-button green"></button>
  </div>
</template>

<style scoped>
.buttons {
  display: flex;
  gap: 20px;
}

.arcade-button {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: none;
  box-shadow: 0 4px 0 #222;
  cursor: pointer;
  transition: transform 0.1s, box-shadow 0.1s;
}

.arcade-button:active {
  transform: translateY(4px);
  box-shadow: 0 0 0 #222;
}

.red {
  background: #ff4444;
  box-shadow: 0 4px 0 #990000;
}

.blue {
  background: #4488ff;
  box-shadow: 0 4px 0 #003399;
}

.green {
  background: #44ff44;
  box-shadow: 0 4px 0 #006600;
}
</style>
