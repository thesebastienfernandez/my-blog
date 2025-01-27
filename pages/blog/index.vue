<template>
    <div>
        <h1>Articles</h1>
        <section id="articles">
            <article v-for="post in posts" :key="post.id">
                <h2>{{ post.title }}</h2>
                <div class="image"></div>
                <p>{{ post.body.slice(0, 200) }}</p>
                <NuxtLink :to="`/blog/${post.id}`"><button>Lire la suite</button></NuxtLink>
            </article>
        </section>
        
    </div>
</template>

<script setup>
const {data: posts} = await useFetch("https://jsonplaceholder.typicode.com/posts?_limit=10")
</script>

<style scoped>
#articles {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    padding: 4em;
    gap: 1em;
}
.image {
    margin: 0 auto;
    background-color: blue;
    width: 30em;
    height: 15em;
}

</style>