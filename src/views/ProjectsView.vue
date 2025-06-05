<script setup>
import { ref, computed, onMounted, onBeforeUnmount, watch } from 'vue';
import TempNavBar from '@/components/TempNavBar.vue';
import ProjectCard from '@/components/ProjectCard.vue';
import projects from '@/data/projects.json';

const selectedIndex = ref(projects.length + Math.floor(projects.length / 2));
const carousel = ref(null);
const viewport = ref(null);

const CARD_WIDTH = 250 + 50;

const duplicatedProjects = [...projects, ...projects, ...projects];
const totalLength = duplicatedProjects.length;

const skipTransition = ref(false);

const isAnimating = ref(false);

function prev() {
  if (isAnimating.value) return;
  
  if (selectedIndex.value > 0) {
    isAnimating.value = true;
    skipTransition.value = false;
    selectedIndex.value--;
    setTimeout(() => {
      isAnimating.value = false;
    }, 500);
  } else {
    isAnimating.value = true;
    skipTransition.value = false;
    selectedIndex.value = totalLength - 1;
    setTimeout(() => {
      skipTransition.value = true;
      selectedIndex.value = selectedIndex.value - projects.length;
      setTimeout(() => {
        skipTransition.value = false;
        isAnimating.value = false;
      }, 50);
    }, 500);
  }
}

function next() {
  if (isAnimating.value) return;
  
  if (selectedIndex.value < totalLength - 1) {
    isAnimating.value = true;
    skipTransition.value = false;
    selectedIndex.value++;
    setTimeout(() => {
      isAnimating.value = false;
    }, 500);
  } else {
    isAnimating.value = true;
    skipTransition.value = false;
    selectedIndex.value = 0;
    setTimeout(() => {
      skipTransition.value = true;
      selectedIndex.value = selectedIndex.value + projects.length;
      setTimeout(() => {
        skipTransition.value = false;
        isAnimating.value = false;
      }, 50);
    }, 500);
  }
}

const carouselStyle = computed(() => {
  if (!viewport.value) return {};
  
  const viewportWidth = viewport.value.offsetWidth;
  const initialOffset = (viewportWidth - CARD_WIDTH) / 2;
  const cardOffset = selectedIndex.value * -CARD_WIDTH;
  const translateX = initialOffset + cardOffset;
  
  return {
    transform: `translate3d(${translateX}px, 0, 0)`,
    transition: skipTransition.value ? 'none' : 'transform 0.5s cubic-bezier(0.4, 0.0, 0.2, 1)',
    'backface-visibility': 'hidden',
    'will-change': 'transform'
  };
});

function checkPosition() {
  if (selectedIndex.value >= (2 * projects.length)) {
    setTimeout(() => {
      skipTransition.value = true;
      selectedIndex.value = selectedIndex.value - projects.length;
      setTimeout(() => {
        skipTransition.value = false;
      }, 50);
    }, 500);
  }
  if (selectedIndex.value < projects.length) {
    setTimeout(() => {
      skipTransition.value = true;
      selectedIndex.value = selectedIndex.value + projects.length;
      setTimeout(() => {
        skipTransition.value = false;
      }, 50);
    }, 500);
  }
}

onMounted(() => {
  window.addEventListener('resize', () => selectedIndex.value = selectedIndex.value);
});
onBeforeUnmount(() => {
  window.removeEventListener('resize', () => selectedIndex.value = selectedIndex.value);
});

watch(selectedIndex, () => {
  checkPosition();
});
</script>

<template>
  <main>
    <TempNavBar />
    <div class="carousel-container">
      <button class="carousel-arrow left" @click="prev" aria-label="Précédent">&#8592;</button>
      <div class="carousel-viewport" ref="viewport">
        <div class="projects-carousel" :style="carouselStyle" ref="carousel">
          <ProjectCard
            v-for="(project, i) in duplicatedProjects"
            :key="i"
            :project="project"
            :class="{ selected: i === selectedIndex }"
          />
        </div>
      </div>
      <button class="carousel-arrow right" @click="next" aria-label="Suivant">&#8594;</button>
    </div>
  </main>
</template>

<style scoped>
.carousel-container {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  width: 100%;
  min-height: 420px;
}

.carousel-viewport {
  width: 80vw;
  max-width: 1100px;
  overflow: hidden;
  position: relative;
  padding: 32px 0;
}

.projects-carousel {
  display: flex;
  gap: 50px;
  will-change: transform;
  width: max-content;
}

.carousel-arrow {
  background: #2d004d;
  color: #ffe066;
  border: none;
  font-size: 2.5em;
  cursor: pointer;
  border-radius: 50%;
  width: 56px;
  height: 56px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 12px #ff2d55aa;
  transition: background 0.2s;
  z-index: 2;
  padding-bottom: 10px ;
  margin: 20px 20px;
}
.carousel-arrow:hover {
  background: #ff2d55;
  color: #fff;
}
</style>