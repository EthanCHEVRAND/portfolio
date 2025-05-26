<script setup>
import ProjectsView from '@/views/ProjectsView.vue';

defineProps({
    project: Object
}) ;

function getImageUrl(image) {
  if (!image) return '';
  return new URL(`../assets/images/${image}`, import.meta.url).href;
}
</script>

<template>
    <div class="card">
        <h3 class="project-title">{{ project.title }}</h3>
        <img v-if="project.image" :src="getImageUrl(project.image)" :alt="project.title" class="project-image">
        <div class="after-image">
            <router-link :to="{ name: 'project-details', params: { id: project.id }}" class="learn-more">
                Voir plus
            </router-link>
            <a v-if="project.github" :href="project.github" class="repo" target="_blank" rel="noopener">Voir sur Github</a>
        </div>
    </div>
</template>

<style scoped>
.card {
  background: #2d004d;
  border-radius: 16px;
  box-shadow: 0 0 16px #ff6a0088;
  color: #ffe066;
  width: 250px;
  height: 350px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
}

.project-title {
    text-align: center;
}

.project-image {
  width: 100%;
  height: auto;
  display: block;
  object-fit: cover;
}

.after-image {
    display: flex;
    align-items: center;
    flex-direction: column;
    margin-bottom: 20px ;
    margin-top: 10px ;
}

.learn-more, .repo {
    background-color: #ffe066;
    color: #fe5858;
    border-radius: 10px;
    height: 30px ;
    width: 120px;
    text-decoration: none;
    font-weight: bold;
    margin-top: 10px;  
    padding-top: 5px;
    text-align: center;
    text-shadow: none;
}

.repo {
    width: 175px;
}
</style> 