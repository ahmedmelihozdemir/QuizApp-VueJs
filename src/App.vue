<template>
    <div>
        <nav>
            <router-link class="nav-element" to="/">Home</router-link>
            <router-link class="nav-element" to="/about">About</router-link>
            <router-link class="nav-element" to="/quiz">Quiz</router-link>
        </nav>
        <router-view />
    </div>
</template>

<script>

</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}
body {
    background-color: rgba(61, 9, 125, 0.64);
}
nav {
    padding: 20px;
    background-color: rgba(7, 141, 146, 0.584);
    border-radius: 10px;
    margin: 5px 5px 15px 5px;
    a {
        font-weight: bold;
        color: #83aedc;
        margin: 20px;
        text-decoration: none;

        &.router-link-exact-active {
            color: #42b983d0;
        }
    }
}
.nav-element:hover {
    border-radius: 10px;
    padding: 10px;
    background-color: #c50d85a3;
    color: #18b7d6;
}
</style>
