<script setup>
import TempNavBar from '@/components/TempNavBar.vue';
</script>

<template>
  <div class="about">
    <TempNavBar />
    <h1>A propos de moi</h1>
    <div class="identification">
      <div class="left-side">
        <!--<img src="#" alt="my photo" class="profile-picture">-->
        <span>Ethan CHEVRAND, 17 ans</span>
        <span>Niveau d'étude actuel : BUT Informatique, 1ere année</span>
      </div>
      <div class="right-side">
        <span>ethan.chevrand987@gmail.com</span>
        <span><img src="../assets/images/icons/github-icon.png" alt="github logo" style="width: 32px; height: 32px;"> EthanCHEVRAND</span>
        <span><img src="../assets/images/icons/discord-icon.png" alt="discord logo" style="width: 32px; height: 32px;"> @zespatule</span>
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
      <br>En dehors du dev, je suis également musicien, danseur et sportif. J'aime la culture geek en général.  
    </div>
  </div>
</template>

<style scoped>
h1 {
  margin-left: 10px;
  color: #ffe066;
  text-shadow: 
    0 0 4px #ff2d55,
    0 0 8px #ff6a00;
}

.identification {
  display: flex;
  flex-direction: row; /* Change to row to place left and right side next to each other */
  justify-content: space-between; /* Spaces the left and right sides */
  margin: 20px;
  padding: 20px;
}

.left-side, .right-side {
  display: flex;
  flex-direction: column;
  gap: 1em; /* Adds vertical spacing between elements */
}

.right-side span, .left-side span {
  display: flex;
  align-items: center;
  gap: 0.5em;
  color: #ffe066;
}

.description {
  padding: 20px;
  margin: 20px;
  outline: 2px solid #ffba66;
  border-radius: 6px;
  text-align: justify;
  color: #ffe066;
}
</style>
