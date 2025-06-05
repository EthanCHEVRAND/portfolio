<script setup>
import { computed } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import TempNavBar from '@/components/TempNavBar.vue';
import projects from '@/data/projects.json';

const route = useRoute();
const router = useRouter();

const project = computed(() => {
  return projects.find(p => p.id === route.params.id);
});

function getImageUrl(image) {
  return new URL(`../assets/images/${image}`, import.meta.url).href;
}

function goBack() {
  router.back();
}

const sortedContent = computed(() => {
  if (!project.value?.content) return [];
  return [...project.value.content].sort((a, b) => a.order - b.order);
});
</script>

<template>
  <TempNavBar />
  <main class="project-detail">
    
    
    <div v-if="project" class="project-content">
      <button @click="goBack" class="back-button">← Retour</button>
      <h1>{{ project.title }}</h1>

      <!-- Contenu mélangé -->
      <div class="mixed-content">
        <template v-for="(item, index) in sortedContent" :key="index">
          <!-- Image -->
          <div v-if="item.type === 'image'" class="image-container">
            <img :src="getImageUrl(item.url)" :alt="item.desc">
            <p class="image-description">{{ item.desc }}</p>
          </div>

          <!-- Description -->
          <section v-else-if="item.type === 'description'" class="description-section">
            <h2>{{ item.title }}</h2>
            <p>{{ item.desc }}</p>
          </section>

          <!-- Button -->
          <section v-else-if="item.type === 'button'" class="button-section">
            <a :href="item.url" target="_blank" rel="noopener" class="button">{{ item.text }}</a>
          </section>
        </template>
      </div>

      <div class="github-link-container">
        <a v-if="project.github" 
           :href="project.github" 
           target="_blank" 
           rel="noopener"
           class="github-link">
          Voir sur Github
        </a>
      </div>
    </div>
  </main>
</template>

<style scoped>
.project-detail {
  color: #ffe066;
  padding: 2em;
}

.project-content {
  max-width: 1200px;
  margin: 0 auto;
}

.image-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2em;
  margin: 2em 0;
}

.image-container img {
  width: 70%;
  height: auto;
  border-radius: 8px;
}

.image-description {
  margin-top: 1em;
  text-align: justify;
}

.github-link-container {
  display: flex;
  justify-content: center;
  width: 100%;
}

.github-link {
  display: inline-block;
  margin-top: 2em;
  padding: 1em 2em;
  background: linear-gradient(160deg, #ff6a00 0%, #ff2d55 100%);
  color: #ffe066;
  text-decoration: none;
  border-radius: 8px;
  font-size: 1.1rem;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
  box-shadow: 
    0 0 20px #ff2d55aa,
    0 0 40px #ff6a0055,
    0 1px 0 #fff4 inset;
  border: 2px solid #ffe066;
  transition: all 0.3s ease;
}

.github-link:hover {
  transform: translateY(-2px);
  box-shadow: 
    0 0 25px #ff2d55cc,
    0 0 50px #ff6a0077,
    0 1px 0 #fff6 inset;
  text-shadow: 
    0 0 8px #ffe066,
    0 0 12px #fff;
}

.github-link:active {
  transform: translateY(1px);
  box-shadow: 
    0 0 15px #ff2d55aa,
    0 0 30px #ff6a0055;
}

.back-button {
  margin: 2em 0;
  padding: 0.8em 1.5em;
  background: #2d004d;
  color: #ffe066;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-family: inherit;
  font-size: 1rem;
  box-shadow: 0 0 12px #ff2d55aa;
  transition: all 0.2s ease;
}

.back-button:hover {
  background: #ff2d55;
  color: #fff;
  box-shadow: 0 0 16px #ff6a00;
}

.mixed-content {
  display: flex;
  flex-direction: column;
  gap: 2em;
  margin: 2em 0;
}

.button-section {
  display: flex;
  justify-content: center;
  margin: 2em 0;
}

.button {
  padding: 1em 2em;
  background: linear-gradient(160deg, #ff6a00 0%, #ff2d55 100%);
  color: #ffe066;
  text-decoration: none;
  border-radius: 8px;
  font-size: 1.1rem;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
  box-shadow: 
    0 0 20px #ff2d55aa,
    0 0 40px #ff6a0055,
    0 1px 0 #fff4 inset;
  border: 2px solid #ffe066;
  transition: all 0.3s ease;
}

.button:hover {
  transform: translateY(-2px);
  box-shadow: 
    0 0 25px #ff2d55cc,
    0 0 50px #ff6a0077,
    0 1px 0 #fff6 inset;
  text-shadow: 
    0 0 8px #ffe066,
    0 0 12px #fff;
}

.button:active {
  transform: translateY(1px);
  box-shadow: 
    0 0 15px #ff2d55aa,
    0 0 30px #ff6a0055;
}
</style>