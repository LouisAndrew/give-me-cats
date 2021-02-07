<template>
    <div class="gifs">
        <h1 v-bind:class="classes.heading">Cute cat gifs 📹</h1>
        <p v-bind:class="classes.text">Click to enjoy random cat gifs.</p>
        <div class="cat-img">
            <Content
                :setPicsCount="setGifsCount"
                :onClick="fetchGifs"
                :urls="urls"
                :count="gifsCount"
                contentType="GIF"
                v-if="!isLoading"
            />
        </div>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';
import axios from 'axios';

// eslint-disable-next-line no-unused-vars
import { Classes } from '@/types';
import Content from './Content.vue';

const GifsProps = Vue.extend({
    props: {
        classes: Object as () => Classes,
    },
    components: {
        Content,
    },
});

@Component
export default class Gifs extends GifsProps {
    endpoint = process.env.VUE_APP__ENDPOINT;
    isLoading = false;
    urls: string[] = [];
    gifsCount = 1;

    created() {
        this.fetchGifs();
    }

    setGifsCount(count: number) {
        this.gifsCount = count;
    }

    async fetchGifs() {
        this.isLoading = true;
        try {
            const res = await axios(
                `${this.endpoint}?mime_types=gif&limit=${this.gifsCount}`,
                {
                    headers: {
                        'x-api-key': process.env.VUE_APP_API_KEY,
                    },
                }
            );
            const { data } = await res;

            this.urls = await data.map((dt: { url: string }) => dt.url);
        } catch (e) {
            console.error(e);
        } finally {
            this.isLoading = false;
        }
    }
}
</script>

<style lang="scss" scoped></style>
