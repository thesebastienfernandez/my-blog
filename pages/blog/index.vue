<template>
    <div>
        <h1>Articles</h1>
        <article v-for="post in posts" :key="post.id">
            <h2>{{ post.title }}</h2>
            <p>{{ post.body.slice(0, 200) }}</p>
            <NuxtLink :to="`/blog/${post.id}`">Lire la suite</NuxtLink>
        </article>
    </div>
</template>

<script setup>
const {data: posts} = await useFetch("https://jsonplaceholder.typicode.com/posts?_limit=10")
</script>