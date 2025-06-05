<script setup>
import { ref, onMounted } from 'vue';
import TempNavBar from '@/components/TempNavBar.vue';
import Skill from '@/components/Skill.vue';
import skills from '@/data/skills.json';

onMounted(() => {
  console.log('TempNavBar component:', TempNavBar);
  console.log('Skills component:', Skill);
});
</script>

<template>
  <main class="skills-view">
    <TempNavBar />
    <div class="skills-container">
      <div class="skills-grid">
        <Skill 
          v-for="skill in skills" 
          :key="skill.id" 
          :skill="skill"
        />
      </div>
    </div>
  </main>
</template>

<style scoped>
.skills-view {
  min-height: 100vh;
}

.skills-container {
  padding: 2em;
  color: #ffe066;
}

h1 {
  text-align: center;
  margin-bottom: 0.5em;
  font-size: 2.5em;
  text-shadow: 
    0 0 4px #ff2d55,
    0 0 8px #ff6a00;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 2em;
  max-width: 1000px;
  margin: 0 auto;
  padding: 2em;
}
</style>