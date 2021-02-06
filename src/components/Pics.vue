<template>
    <div class="pics">
        <h1 v-bind:class="classes.heading">Cute cat pics 📷</h1>
        <p v-bind:class="classes.text">
            Click one of the button below to continue!
        </p>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';

// eslint-disable-next-line no-unused-vars
import { Classes } from '@/types';

const PicsProps = Vue.extend({
    props: {
        classes: Object as () => Classes,
    },
});

@Component
export default class Pics extends PicsProps {}
</script>

<style lang="scss" scoped></style>
