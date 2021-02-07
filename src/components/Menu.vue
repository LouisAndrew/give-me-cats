<template>
    <div class="menu">
        <h1 v-bind:class="classes.heading">Hey there! 👋</h1>
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

const MenuProps = Vue.extend({
    props: {
        classes: {
            type: Object as () => Classes,
        },
    },
});

@Component
export default class Menu extends MenuProps {}
</script>

<style scoped></style>
