<template>
    <div id="app">
        <img alt="Vue logo" src="./assets/logo.png">
        <h1>Todo application</h1>
        <hr>
        <router-view/>
    </div>
</template>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    form {
        margin-left: auto;
        margin-right: auto;
        width: 30%;
    }
</style>
