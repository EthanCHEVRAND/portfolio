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
    <div class="navigation-p">
      <p>[tab] : retourner à la navigation</p>
      <p>[arrows] : bouger le curseur</p>
      <p>[scroll] or [scroll-bar] : faire défiler</p>
      <p>[enter] : séléctionner</p>
    </div>

  </main>
</template>

<style scoped>
h1 {
  margin-top: 20px ;
  text-align: center ;
  font-size: 1.5em ;
}

.navigation-p {
  margin-left: 80px ;
}
</style>