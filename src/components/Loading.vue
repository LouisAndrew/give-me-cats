<template>
    <div class="loader">
        <Lottie :options="defaultOptions" :height="256" :width="256" />
    </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import Lottie from 'vue-lottie/src/lottie.vue';

// Animation json files from https://lottiefiles.com
// @ts-ignore
import animData from './assets/loading-anim.json';

// @ts-ignore
@Component({
    components: {
        Lottie,
    },
})
export default class Loading extends Vue {
    animationData = animData;

    // options for lottie files.
    defaultOptions = {
        animationData: this.animationData,
        animationSpeed: 1,
    };
}
</script>

<style scoped></style>
