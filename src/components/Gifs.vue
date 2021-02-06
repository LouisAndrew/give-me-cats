<template>
    <div class="gifs">
        <h1 v-bind:class="classes.heading">Cute cat gifs 📹</h1>
        <p v-bind:class="classes.text">
            Click one of the button below to continue!
        </p>
        <div class="cat-img">
            <img v-if="shouldRender" v-bind:src="url" alt="" />
            <button @click="fetchImg">Fetch</button>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';

// eslint-disable-next-line no-unused-vars
import { Classes } from '@/types';

const GifsProps = Vue.extend({
    props: {
        classes: Object as () => Classes,
    },
});

@Component
export default class Gifs extends GifsProps {
    endpoint = process.env.THE_CAT_ENDPOINT;
    shouldRender = true;

    get url() {
        return `${this.endpoint}`;
    }

    async fetchImg() {
        fetch(this.endpoint, {
            method: 'GET',
            headers: {
                'x-api-key': process.env.THE_CAT_API_KEY,
            },
        })
            .then(dt => dt.json())
            .then(s => console.log(s));
    }
}
</script>

<style lang="scss" scoped></style>
