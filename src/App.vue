<template>
    <div
        id="app"
        class="flex items-start justify-center h-screen flex-nowrap pt-6"
    >
        <div class="wrapper h-content">
            <Menu v-if="appState === States.MAIN" v-bind:classes="classes" />
            <Pics v-if="appState === States.PICS" v-bind:classes="classes" />
            <Gifs
                v-else-if="appState === States.GIFS"
                v-bind:classes="classes"
            />

            <div class="buttons flex w-full justify-evenly mt-3">
                <button
                    :class="buttonClass"
                    v-if="appState !== States.MAIN"
                    @click="goToMain"
                >
                    Main screen
                </button>
                <button
                    :class="buttonClass"
                    v-if="appState !== States.PICS"
                    @click="goToPics"
                >
                    Pics
                </button>
                <button
                    :class="buttonClass"
                    v-if="appState !== States.GIFS"
                    @click="goToGifs"
                >
                    Gifs
                </button>
            </div>
        </div>
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
        heading:
            'text-3xl font-bold tracking-wider font-sans whitespace-nowrap flex-shrink-0 text-center',
        text:
            'mt-4 text-gray-500 tracking-wider font-sans flex-shrink-0 text-center',
    };

    buttonClass =
        'px-4 py-3 bg-green-100 text-sm font-bold text-green-500 rounded-xl w-full mx-1 transition duration-200 hover:bg-green-400 hover:text-white';

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
}
</style>
