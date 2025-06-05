<template>
  <div 
    ref="skillCard"
    class="skill-card"
    @mouseenter="isHovered = true"
    @mouseleave="isHovered = false"
  >
    <div class="skill-icon">
      <img :src="getImageUrl(skill.icon)" :alt="skill.name">
    </div>
    <h3>{{ skill.name }}</h3>
    
    <!-- Ajout des points de niveau -->
    <div class="level-dots">
      <span 
        v-for="n in 5" 
        :key="n"
        class="dot"
        :class="{ filled: n <= skill.level }"
      ></span>
    </div>
    
    <div 
      v-if="isHovered" 
      class="skill-details"
      :class="{ 'show-left': showLeft }"
    >
      <p class="description">{{ skill.description }}</p>
      <ul class="details-list">
        <li v-for="detail in skill.details" :key="detail">
          {{ detail }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const props = defineProps({
  skill: {
    type: Object,
    required: true
  }
});

const skillCard = ref(null);
const isHovered = ref(false);
const showLeft = ref(false);

function getImageUrl(icon) {
  return new URL(`../assets/images/icons/${icon}`, import.meta.url).href;
}

onMounted(() => {
  const checkPosition = () => {
    if (!skillCard.value) return;
    const rect = skillCard.value.getBoundingClientRect();
    const parentRect = skillCard.value.closest('.skills-grid').getBoundingClientRect();
    // Utilise la position relative à la grille plutôt que la fenêtre
    showLeft.value = (rect.left - parentRect.left) > parentRect.width / 2;
  };

  checkPosition();
  window.addEventListener('resize', checkPosition);

  // Nettoyage de l'event listener
  onBeforeUnmount(() => {
    window.removeEventListener('resize', checkPosition);
  });
});
</script>

<style scoped>

.skill-card {
  position: relative;
  width: 120px;
  min-height: 120px;
  padding: 0.5em;
  border-radius: 12px;
  text-align: center;
  cursor: pointer;
  transition: transform 0.3s, box-shadow 0.3s;
}

.skill-card:hover {
  transform: translateY(-5px);
  box-shadow: 
    0 0 20px #ff2d55aa,
    0 0 40px #ff6a0055;
  z-index: 10;
}

.skill-icon img {
  width: 96px;
  height: 96px;
  margin-bottom: 0.5em;
}

.skill-details {
  position: absolute;
  top: 50%;
  left: calc(100% + 10px);
  transform: translateY(-50%);
  background: #2d004d;
  padding: 1.5em;
  border-radius: 8px;
  box-shadow: 
    0 0 20px rgba(0,0,0,0.5),
    0 0 30px #ff2d55aa;
  z-index: 11;
  width: 250px;
  pointer-events: none;
  opacity: 0;
  animation: fadeIn 0.3s forwards;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-50%) translateX(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(-50%) translateX(0);
  }
}

.skill-details.show-left {
  left: auto;
  right: calc(100% + 10px);
  animation: fadeInLeft 0.3s forwards;
}

@keyframes fadeInLeft {
  from {
    opacity: 0;
    transform: translateY(-50%) translateX(20px);
  }
  to {
    opacity: 1;
    transform: translateY(-50%) translateX(0);
  }
}

.skill-details::before {
  content: '';
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  border: 10px solid transparent;
}

.skill-details:not(.show-left)::before {
  left: -20px;
  border-right-color: #2d004d;
}

.skill-details.show-left::before {
  right: -20px;
  border-left-color: #2d004d;
}

.description {
  margin-bottom: 1em;
  font-size: 0.9em;
}

.details-list {
  list-style: none;
  padding: 0;
  text-align: left;
  font-size: 0.8em;
}

.level-dots {
  display: flex;
  justify-content: center;
  gap: 4px;
  margin-top: 1em;
}

.dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #4d0066;
  border: 1px solid #ff6a00;
}

.dot.filled {
  background: #ff6a00;
  box-shadow: 0 0 8px #ff2d55;
}

.skills-grid:has(.skill-card:hover) .skill-card:not(:hover) {
  filter: blur(2px);
  opacity: 0.7;
  transform: scale(0.95);
}

.skills-grid {
  gap: 3em 15em;
}
</style>