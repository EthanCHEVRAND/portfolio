<template>
    <nav>
        <ul>
            <li>
                <router-link class="link" to="/">Home</router-link>
            </li>
            <li>
                <router-link class="link" to="/projects">Projets</router-link>
            </li>
            <li>
                <router-link class="link" to="/about">A propos de moi</router-link>
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
</style>