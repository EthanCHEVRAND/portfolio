<script setup>
import TempNavBar from '@/components/TempNavBar.vue';
</script>

<template>
  <main>
    <TempNavBar />
    <h1>Bienvenue sur le portfolio de Ethan CHEVRAND</h1>
    <br>
    <!-- pour naviguer section : arrows to move, tab to return to nav bar, enter to select-->
    <h3>Pour naviguer : </h3>
    <div class="navigation-p" id="main-content" tabindex="-1">
      <p class="arcade-focusable" tabindex="0">[tab] : retourner à la navigation</p>
      <p class="arcade-focusable" tabindex="0">[arrows] : bouger le curseur</p>
      <p class="arcade-focusable" tabindex="0">[scroll] or [scroll-bar] : faire défiler</p>
      <p class="arcade-focusable" tabindex="0">[enter] : séléctionner</p>
      <p class="arcade-focusable" tabindex="0">[souris] : comme sur n'importe quel site</p>
    </div>
  </main>
</template>

<style scoped>
h1 {
  margin-top: 20px ;
  text-align: center ;
  font-size: 1.5em ;
}

h3 {
  margin-left: 20px;
}

.navigation-p {
  margin-left: 80px ;
}
</style>