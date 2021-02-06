<template>
    <div id="app">
        <img alt="Vue logo" src="./assets/logo.png" />
        <h1>Test</h1>
        <Menu v-if="appState === States.MAIN" />
        <Pics v-if="appState === States.PICS" />
        <Gifs v-else-if="appState === States.GIFS" />

        <button v-if="appState !== States.MAIN" @click="goToMain">
            Go to main
        </button>
        <button v-if="appState !== States.PICS" @click="goToPics">
            Go to pics
        </button>
        <button v-if="appState !== States.GIFS" @click="goToGifs">
            Go to gifs
        </button>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

import Menu from './components/Menu.vue';
import Pics from './components/Pics.vue';
import Gifs from './components/Gifs.vue';
import { AppStates } from './enums';

@Component({
    components: {
        Menu,
        Pics,
        Gifs,
    },
})
export default class App extends Vue {
    private States = AppStates;
    appState: AppStates = this.States.MAIN;

    goToMain() {
        this.appState = this.States.MAIN;
    }

    goToPics() {
        this.appState = this.States.PICS;
    }

    goToGifs() {
        this.appState = this.States.GIFS;
    }
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
