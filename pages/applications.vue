<template>
    <div>
        <header>
            <h1>Outils pratiques</h1>
        </header>
        <main>
            <ul>
                <li><NuxtLink to="/globalQuiz">Quiz</NuxtLink> (Testez vos connaissances pratiques)</li>
                <li><NuxtLink to="/todoList">Todolist</NuxtLink> (Exemple de routine quotidienne)</li>
            </ul>
        </main>
    </div>
</template>

<style scoped>
li {
    margin-bottom: 2em;
}

li a {
    text-decoration: underline;
}
</style>