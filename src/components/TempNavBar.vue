<template>
  <nav class="main-navbar">
    <ul>
      <li>
        <router-link class="link arcade-nav-focusable" tabindex="-1" to="/">Accueil</router-link>
      </li>
      <li>
        <router-link class="link arcade-nav-focusable" tabindex="-1" to="/projects">Projets</router-link>
      </li>
      <li>
        <router-link class="link arcade-nav-focusable" tabindex="-1" to="/skills">Compétences</router-link>
      </li>
      <li>
        <router-link class="link arcade-nav-focusable" tabindex="-1" to="/about">A propos de moi</router-link>
      </li>
    </ul>
  </nav>
  <div class="separator"></div>
</template>

<style scoped>
ul {
    display: flex ;
    flex-direction: row;
    justify-content: space-evenly;
    align-items: center;
    list-style-type: none;
}

.link {
    color: #fff ;
    text-decoration: none;
}

.separator {
    width: 100%;
    height: 2px;
    background-image: linear-gradient(to right, rgba(255, 255, 255, 0), #fff,#fff, #fff,  rgba(255, 255, 255, 0));
    margin-top: 10px;
}

.link.arcade-nav-focusable:focus {
  outline: 2px solid #ffe066;
  box-shadow: 0 0 8px #ff2d55, 0 0 16px #ff6a00;
  border-radius: 6px;
}
</style>