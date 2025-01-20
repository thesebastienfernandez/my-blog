<template>
    <nav>  
        <NuxtLink id="logo-div" to="/">
            <img width="30" height="45" src="../../assets/images/skull.png"/>
            <p>Astartesium</p>
        </NuxtLink>
        <NuxtLink to="/blog">Articles</NuxtLink>
        <NuxtLink to="/about">A propos</NuxtLink>
        <NuxtLink to="/applications">Outils</NuxtLink>
    </nav>
</template>

<style scoped>

nav {
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 4em;
    width: 100%;
    background-color: #2ecc71;
    font-size: 1.3em;
    font-weight: bold;
}

nav a {
    color: #ecf0f1;
}

nav a:hover{
    color: black;
    text-decoration: underline;
}

#logo-div {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 8em;
}

</style>



