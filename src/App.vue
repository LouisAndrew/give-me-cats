<template>
    <div
        id="app"
        class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2"
    >
        <Menu v-if="appState === States.MAIN" v-bind:classes="classes" />
        <Pics v-if="appState === States.PICS" v-bind:classes="classes" />
        <Gifs v-else-if="appState === States.GIFS" v-bind:classes="classes" />

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
import Vue from 'vue';
import Component from 'vue-class-component';

import Menu from './components/Menu.vue';
import Pics from './components/Pics.vue';
import Gifs from './components/Gifs.vue';
import { AppStates } from './enums';

import './assets/styles/index.css'; // import tailwind library

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
    classes = {
        heading: 'text-3xl font-bold tracking-wider',
        text: 'mt-4 text-gray-500 tracking-wider',
    };

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
