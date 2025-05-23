<!-- src/layout/ArcadeShell.vue -->
<template>
    <!-- Écran de la borne -->
    <div class="arcade-shell">
      <div class="arcade-screen">
        <router-view />
      </div>
    </div>
    <div class="arcade-buttons-div">
      <div class="arcade-buttons">
        <Stick class="arcade-stick"/>
        <ButtonPanel class="buttons"/>
      </div>
    </div>
</template>

<script setup>
import ButtonPanel from '@/components/ButtonPanel.vue';
import Stick from '@/components/Stick.vue';

</script>

<style scoped>
template {
  display: flex ;
  flex-direction: column;
}

.arcade-shell {
  width: 100% ;
  height: 500px ;
  display: flex;
  justify-content: center;
  margin-top: 5px ;
  margin-bottom: 60px ;
}

.arcade-screen {
  padding: 10px ;
  padding-top: 0px ;
  width: 90%;
  height: 100%;
  background: #000;
  border: 20px solid #222;
  border-radius: 10px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
}

.arcade-buttons-div {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 120px;
}

.arcade-buttons {
  width: 95% ;
  height: 100% ;
  background-color: #fff;
  display: flex;
  justify-content: space-around;
}

.buttons {
  margin-top: 30px ;
}

.arcade-screen {
  width: 90%;
  height: 100%;
  background: #111;
  border: 20px solid #222;
  border-radius: 10px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.5), 0 0 60px #00ffea33 inset;
  position: relative;
  overflow: hidden;
}

.arcade-screen::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: 8px;
  background: radial-gradient(ellipse at 60% 40%, #222 60%, transparent 100%);
  opacity: 0.5;
  pointer-events: none;
}

.arcade-screen::after {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: 8px;
  background: repeating-linear-gradient(
    to bottom,
    transparent 0px,
    rgba(255,255,255,0.03) 2px,
    transparent 4px
  );
  pointer-events: none;
  z-index: 2;
}

</style>
