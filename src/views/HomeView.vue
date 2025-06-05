<script setup>
import TempNavBar from '@/components/TempNavBar.vue';
</script>

<template>
  <main>
    <TempNavBar />
    <h1>Ethan CHEVRAND - Gamedev en devenir ?</h1>
    <h2>Etudiant en BUT informatique, passioné par le jeu vidéo</h2>
    <h3>UE choisies : </h3>
    <ul>
      <li>UE 1 - Réaliser un développement d'application</li>
      <li>UE 4 - Gérer des données de l'information</li>
    </ul>
    <h3>Quels sont les savoirs et savoir-faire requis ?</h3>
    <ul>
      <li>
        <h4>UE 1</h4>
        <ul>
          <li>Avoir un pensée algorithmique</li>
          <li>Comprendre les bases du développement orienté objet</li>
          <li>Comprendre le langage Java</li>
          <li>Connaître les bases du développemen web (HTML / CSS)</li>
          <li>Connaître le paradigme MVC (Modèle / Vue / Controlleurs)</li>
          <li>Savoir effectuer des tests unitaires</li>
        </ul>
      </li>

      <li>
        <h4>UE 4</h4>
        <ul>
          <li>Concevoir une base de donnée efficace (MCD)</li>
          <li>Comprendre le SQL (MySQL/MariaDB dans notre cas)</li>
          <li>Savoir créer une base donnée</li>
          <li>Savoir exploiter une base de donnée</li>
          <li>Savoir exploiter des données (stats)</li>
        </ul>
      </li>
    </ul>
  </main>
</template>

<style scoped>
h1 {
  margin-top: 20px ;
  text-align: center ;
  font-size: 1.5em ;
}

h2 {
  text-align: center ;
  font-size: 1.2em ;
}

h3 {
  margin-left: 20px;
  margin-bottom: 4px;
}

h4 {
  margin-bottom: 4px ;
}
</style>