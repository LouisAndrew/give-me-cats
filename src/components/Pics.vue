<template>
    <div class="pics flex flex-col items-center">
        <h1 v-bind:class="classes.heading">Cute cat pics 📷</h1>
        <p v-bind:class="classes.text">
            Click to enjoy some random cat images
        </p>
        <div class="cat-img">
            <Content
                :setPicsCount="setPicsCount"
                @click="fetchImg"
                :urls="urls"
                :count="picsCount"
                contentType="PIC"
                v-if="!isLoading"
            />
            <Loading v-else-if="isLoading" />
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
import Loading from './Loading.vue';

const PicsProps = Vue.extend({
    props: {
        classes: Object as () => Classes,
    },
});

@Component({
    components: {
        Content,
        Loading,
    },
})
export default class Pics extends PicsProps {
    endpoint = process.env.VUE_APP__ENDPOINT;
    isLoading = true;
    urls: string[] = [];
    picsCount = 1;

    created() {
        this.fetchImg();
    }

    setPicsCount(count: number) {
        this.picsCount = count;
    }

    async fetchImg() {
        this.isLoading = true;
        try {
            const res = await axios(
                `${this.endpoint}?mime_types=png&limit=${this.picsCount}`,
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
