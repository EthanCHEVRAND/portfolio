<!-- src/layout/ArcadeShell.vue -->
<template>
    <!-- Écran de la borne -->
    <div class="arcade-shell">
      <div class="arcade-screen">
        <canvas v-if="!hideSnow" ref="snowCanvas" class="snow-canvas"></canvas>
        <router-view />
      </div>
    </div>
    <div class="arcade-buttons-div">
      <div class="arcade-buttons">
        <!--Stick class="arcade-stick"/-->
        <!--ButtonPanel class="buttons"/-->
      </div>
    </div>
</template>

<script setup>
import { onMounted, onBeforeUnmount, ref, computed, watch } from 'vue';
import { useRoute } from 'vue-router';
import ButtonPanel from '@/components/ButtonPanel.vue';
import Stick from '@/components/Stick.vue';

const route = useRoute();
const snowCanvas = ref(null);
let animationFrameId = null; // Pour pouvoir annuler l'animation

// Vérifie si on est sur la page de détails
const hideSnow = computed(() => {
  // On ne veut PAS de neige sur la page de détails (project-details)
  return route.name === 'project-details';
});

// Fonction pour initialiser l'effet de neige
function initSnowEffect() {
  const canvas = snowCanvas.value;
  if (!canvas || hideSnow.value) return;

  const ctx = canvas.getContext('2d');
  let width, height;

  function resize() {
    width = canvas.offsetWidth;
    height = canvas.offsetHeight;
    canvas.width = width;
    canvas.height = height;
  }

  resize();
  window.addEventListener('resize', resize);

  function drawSnow() {
    ctx.clearRect(0, 0, width, height);
    for (let i = 0; i < width * height * 0.018; i++) {
      const x = Math.random() * width;
      const y = Math.random() * height;
      const gray = Math.random() * 255;
      ctx.fillStyle = `rgba(${gray},${gray},${gray},${Math.random() * 0.35 + 0.18})`;
      ctx.fillRect(x, y, 1.2, 1.2);
    }
    animationFrameId = requestAnimationFrame(drawSnow);
  }
  
  // Démarrer l'animation
  drawSnow();
}

// Fonction pour arrêter l'effet de neige
function stopSnowEffect() {
  if (animationFrameId) {
    cancelAnimationFrame(animationFrameId);
    animationFrameId = null;
  }
}

// Surveiller les changements de route
watch(
  () => route.name,
  () => {
    if (hideSnow.value) {
      stopSnowEffect();
    } else {
      initSnowEffect();
    }
  }
);

onMounted(() => {
  initSnowEffect();
});

onBeforeUnmount(() => {
  stopSnowEffect();
  // Important : le listener doit être sur window, pas sur .main-navbar
  window.removeEventListener('keydown', handleNavKey);
  window.removeEventListener('keydown', handleKey);
  window.removeEventListener('keydown', handleGlobalTab);
});
</script>

<style scoped>

.arcade-shell {
  width: 100%;
  height: 75vh;
  display: flex;
  justify-content: center;
  padding-top: 5px;
  /* Violet rétro wave avec effet néon */
  background: #1a0033;
}

.arcade-screen {
  position: relative;
  width: 90%;
  height: 90%;
  background: linear-gradient(160deg, #2d004d 0%, #0a001a 100%);
  border: 12px solid #ff6a00;
  border-radius: 18px;
  box-shadow:
    0 0 32px #ff2d55cc,
    0 0 48px #ffe06655 inset,
    0 0 16px #ff6a00cc,
    0 0 10px #000a;
  overflow-y: auto; /* Permet le scroll vertical */
  overflow-x: hidden; /* Cache le scroll horizontal */
  padding: 10px;
  /* Stylise la barre de défilement */
  scrollbar-width: thin;
  scrollbar-color: #ff6a00 #2d004d;
}

/* Style de la barre de défilement pour Chrome/Safari/Edge */
.arcade-screen::-webkit-scrollbar {
  width: 8px;
}

.arcade-screen::-webkit-scrollbar-track {
  background: #2d004d;
}

.arcade-screen::-webkit-scrollbar-thumb {
  background: #ff6a00;
  border-radius: 4px;
}

.arcade-screen::-webkit-scrollbar-thumb:hover {
  background: #ff2d55;
}

.snow-canvas {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 3;
  mix-blend-mode: lighten;
  opacity: 0.32;
}

/* Texte rétro wave néon */
.arcade-screen,
.arcade-buttons,
.arcade-button {
  font-family: 'Share Tech Mono', 'VT323', 'Press Start 2P', monospace, sans-serif;
  color: #ffe066;
  text-shadow:
    0 0 4px #ff2d55,
    0 0 3px #ff6a00,
    0 0 2px #fff,
    0 0 8px #ffe06677;
  /* Taille de police uniforme pour tous les éléments principaux */
  font-size: 1.15rem;
  line-height: 1.4;
}

/* Pour les boutons, un peu plus grand si besoin */
.arcade-button {
  width: 44px;
  height: 44px;
  background: radial-gradient(circle at 30% 30%, #ffe066 40%, #ff6a00 70%, #ff2d55 100%);
  border: 2px solid #ffe066;
  border-radius: 50%;
  box-shadow:
    0 0 12px #ff2d55cc,
    0 1px 0 #fff4 inset,
    0 0 0 2px #2d004d;
  margin: 0 6px;
  cursor: pointer;
  transition: transform 0.1s, box-shadow 0.1s;
  font-size: 1.25rem;
}

.arcade-button:active {
  transform: scale(0.94);
  box-shadow: 0 1px 3px #000a, 0 0 0 2px #ff6a00;
}

/* Pour les titres éventuels dans arcade-screen */
.arcade-screen h1,
.arcade-screen h2 {
  font-size: 2.5rem;
  font-weight: bold;
  margin-bottom: 0.5em;
  letter-spacing: 0.04em;
}

/* Pour les petits textes ou labels */
.arcade-screen small,
.arcade-buttons small {
  font-size: 1.25rem;
  opacity: 0.85;
}

.arcade-screen::before {
  content: "";
  position: absolute;
  inset: 0;
  pointer-events: none;
  background: repeating-linear-gradient(
    to bottom,
    transparent 0px,
    transparent 2px,
    #ff2d5522 3px,
    transparent 4px
  );
  opacity: 0.07;
  z-index: 2;
}

.arcade-buttons-div {
  height: 25vh;
  width: 100%;
  background: #1a0033;
  display: flex;
  justify-content: center;
  align-items: flex-end;
}

.arcade-buttons {
  display: flex;
  gap: 36px;
  background: linear-gradient(90deg, #2d004d 0%, #ff6a00 60%, #ff2d55 100%);
  border-radius: 24px;
  padding: 24px 48px;
  box-shadow:
    0 0 24px #ff2d55aa,
    0 0 8px #ffe06688;
  align-items: flex-end;
  border: 2px solid #ffe066;
}

.arcade-stick {
  width: 72px;
  height: 140px;
  display: flex;
  align-items: flex-end;
  justify-content: center;
}

.buttons {
  display: flex;
  gap: 16px;
  align-items: flex-end;
}

.arcade-focusable:focus {
  outline: 2px solid #ffe066;
  box-shadow: 0 0 8px #ff2d55, 0 0 16px #ff6a00;
  border-radius: 6px;
}

#main-content:focus {
  outline: 2px solid #ffe066;
  box-shadow: 0 0 8px #ff2d55, 0 0 16px #ff6a00;
}
</style>
