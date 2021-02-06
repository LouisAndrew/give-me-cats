<template>
    <div class="pics">
        <h1 v-bind:class="classes.heading">Cute cat pics 📷</h1>
        <p v-bind:class="classes.text">
            Click one of the button below to continue!
        </p>
        <div class="cat-img">
            <img v-if="!isLoading" v-bind:src="url" alt="" />
            <button @click="fetchImg">Fetch</button>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';
import axios from 'axios';

// eslint-disable-next-line no-unused-vars
import { Classes } from '@/types';

const PicsProps = Vue.extend({
    props: {
        classes: Object as () => Classes,
    },
});

@Component
export default class Pics extends PicsProps {
    endpoint = process.env.VUE_APP__ENDPOINT;
    isLoading = false;
    url = '';

    created() {
        this.fetchImg();
    }

    async fetchImg() {
        this.isLoading = true;
        console.log(process.env.VUE_APP_API_KEY);
        try {
            const res = await axios(`${this.endpoint}?mime_types=png`, {
                headers: {
                    'x-api-key': process.env.VUE_APP_API_KEY,
                },
            });
            const { data } = await res;
            this.url = await data[0].url;
        } catch (e) {
            console.error(e);
        } finally {
            this.isLoading = false;
        }
    }
}
</script>

<style lang="scss" scoped></style>
