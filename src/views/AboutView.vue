<script setup>
import TempNavBar from '@/components/TempNavBar.vue';
</script>

<template>
  <div class="about">
    <TempNavBar />
    <h1>A propos de moi</h1>
    <div class="identification">
      <div class="left-side">
        <img src="#" alt="my photo" class="profile-picture">
        <span>Ethan CHEVRAND, 17 ans</span>
        <span>Niveau d'étude actuel : BUT Informatique, 1ere année</span>
      </div>
      <div class="right-side">
        <span>ethan.chevrand987@gmail.com</span>
        <span><img src="#" alt="github logo"> EthanCHEVRAND</span>
        <span><img src="#" alt="discord logo"> @zespatule</span>
      </div>
    </div>
    <br>
    <div class="description">Passioné d'informatique et de jeux vidéos depuis l'enfance, j'ai créé mes premiers projets
      sur scratch à mes 8 ans, sur mon premier ordinateur.<br>
      Aujourd'hui, je suis en études d'informatique, après avoir 
      eu mon bac général (spécialités Maths et NSI). Je travaille sur 
      des projets personnels, dont un jeu, en plus de mes travaux en tant qu'étudiant.<br>
      Mon objectif principal est de devenir Gamedev, si possible indépendant (étant moi même fan de jeux vidéos indépendants).<br>
      J'essaie également de toucher à du développement web, de la base de données, du développement mobile, du développement d'applications, ... 
    </div>
  </div>
</template>

<style scoped>
h1 {
  margin-left: 10px; 
}

.identification {
  display: flex ;
  flex-direction: column;
  margin-left: 20px; 
}

.description {
  padding: 10px ;
  margin-left: 20px ;
  margin-right: 20px ;
  outline: 2px solid #ffba66;
  border-radius: 6px;
  text-align: justify ;
}
</style>
