<!-- src/layout/ArcadeShell.vue -->
<template>
    <!-- Écran de la borne -->
    <div class="arcade-shell">
      <div class="arcade-screen">
        <canvas ref="snowCanvas" class="snow-canvas"></canvas>
        <div class="scanline"></div>
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
import { onMounted, onBeforeUnmount, ref } from 'vue';
import ButtonPanel from '@/components/ButtonPanel.vue';
import Stick from '@/components/Stick.vue';

const snowCanvas = ref(null);

onMounted(() => {
  // Effet neige/grésillement rétro, plus visible
  const canvas = snowCanvas.value;
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
    // Augmente la densité et l'opacité pour plus de visibilité
    for (let i = 0; i < width * height * 0.018; i++) {
      const x = Math.random() * width;
      const y = Math.random() * height;
      const gray = Math.random() * 255;
      ctx.fillStyle = `rgba(${gray},${gray},${gray},${Math.random() * 0.35 + 0.18})`;
      ctx.fillRect(x, y, 1.2, 1.2);
    }
    requestAnimationFrame(drawSnow);
  }
  drawSnow();

  function handleKey(e) {
    const focusables = Array.from(document.querySelectorAll('.arcade-focusable'));
    const current = document.activeElement;
    let idx = focusables.indexOf(current);

    // Navigation verticale (haut/bas ou Z/S)
    if (['ArrowDown', 's', 'S'].includes(e.key)) idx++;
    if (['ArrowUp', 'z', 'Z'].includes(e.key)) idx--;
    if (idx < 0) idx = focusables.length - 1;
    if (idx >= focusables.length) idx = 0;

    if (
      ['ArrowDown', 'ArrowUp', 'z', 'Z', 's', 'S'].includes(e.key)
      && focusables.length
    ) {
      e.preventDefault();
      focusables[idx].focus();
    }

    // Entrée pour cliquer
    if (e.key === 'Enter' && current.classList.contains('arcade-focusable')) {
      current.click();
    }

    // Tab pour retourner à la barre de navigation
    if (e.key === 'Tab') {
      e.preventDefault();
      const nav = document.querySelector('.main-navbar');
      const firstLink = nav.querySelector('.arcade-nav-focusable');
      if (firstLink) firstLink.focus();
    }
  }

  function handleNavKey(e) {
    const navLinks = Array.from(document.querySelectorAll('.arcade-nav-focusable'));
    const current = document.activeElement;
    let idx = navLinks.indexOf(current);

    if (['ArrowRight', 'd', 'D'].includes(e.key)) idx++;
    if (['ArrowLeft', 'q', 'Q'].includes(e.key)) idx--;
    if (idx < 0) idx = navLinks.length - 1;
    if (idx >= navLinks.length) idx = 0;

    if (
      ['ArrowRight', 'ArrowLeft', 'd', 'D', 'q', 'Q'].includes(e.key)
      && navLinks.length
    ) {
      e.preventDefault();
      navLinks[idx].focus();
    }

    // Entrée pour cliquer sur le lien
    if (e.key === 'Enter' && current.classList.contains('arcade-nav-focusable')) {
      current.click();
    }

    // Tab pour retourner au contenu principal
    if (e.key === 'Tab') {
      e.preventDefault();
      const main = document.getElementById('main-content');
      if (main) main.focus();
    }
  }

  // Ajoute le listener sur la navbar
  const navbar = document.querySelector('.main-navbar');
  if (navbar) navbar.addEventListener('keydown', handleNavKey);

  window.addEventListener('keydown', handleKey);
  onBeforeUnmount(() => {
    if (navbar) navbar.removeEventListener('keydown', handleNavKey);
    window.removeEventListener('keydown', handleKey);
  });
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
  overflow: hidden;
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

.scanline {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 28px;
  left: -28px;
  background: linear-gradient(90deg, transparent 0%, #ff6a00cc 50%, transparent 100%);
  opacity: 0.18;
  z-index: 4;
  animation: scanline-move 30s linear infinite;
}

@keyframes scanline-move {
  0% { left: -28px; }
  100% { left: 100%; }
}

/* Texte rétro wave néon */
.arcade-screen,
.arcade-buttons,
.arcade-button {
  font-family: 'Share Tech Mono', 'VT323', 'Press Start 2P', monospace, sans-serif;
  color: #ffe066;
  text-shadow:
    0 0 8px #ff2d55,
    0 0 4px #ff6a00,
    0 0 2px #fff,
    0 0 16px #ffe06677;
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
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 0.5em;
  letter-spacing: 0.04em;
}

/* Pour les petits textes ou labels */
.arcade-screen small,
.arcade-buttons small {
  font-size: 0.95rem;
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
