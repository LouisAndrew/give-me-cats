<template>
    <div class="content flex flex-col items-center">
        <ul class="content-list flex flex-col items-center">
            <li class="max-w-sm" v-for="url in urls" :key="url">
                <img
                    v-bind:src="url"
                    alt="cat"
                    class="my-6 rounded-xl shadow-2xl"
                />
            </li>
        </ul>
        <h4 class="font-semibold tracking-wider mb-3 font-sans">
            Now showing:
            <input
                :class="
                    `transition duration-200 inline-block w-5 text-center border-b-4 border-solid bg-transparent ${borderClass}`
                "
                type="number"
                :value="num"
                @change="handleChange"
            />
            {{ nowShowing }} of cats
        </h4>
        <h6 class="text-xs mb-4 font-bold text-green-600">
            *number of limited content available: {{ limit }}
        </h6>
        <button
            @click="handleClick"
            class="px-4 py-3 bg-green-400 text-sm font-bold text-white rounded-xl transition duration-200 hover:text-green-200"
        >
            Give me another!
        </button>
    </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator';

@Component
export default class Content extends Vue {
    @Prop({ type: Array, required: true }) urls!: string[];
    @Prop({ type: Function, required: true }) onClick!: () => void;
    @Prop({ type: Function, required: true }) setPicsCount!: (
        count: number
    ) => void;
    @Prop({ type: Number, required: true }) count!: number;
    @Prop({ type: String, required: true }) contentType!: 'GIF' | 'PIC';

    limit = 10;
    limitPassed = false;
    num = 1;

    created() {
        this.num = this.count;
    }

    get nowShowing() {
        return this.contentType === 'GIF' ? 'gifs' : 'pics';
    }

    get borderClass() {
        return this.limitPassed ? 'border-red-500' : 'border-green-500';
    }

    handleClick() {
        this.onClick();
    }

    handleChange(e: any) {
        // this.setPicsCount(parseInt(e.target.value));
        this.num = parseInt(e.target.value);
        if (this.num <= this.limit) {
            this.limitPassed = false;
            this.setPicsCount(this.num);
        } else {
            this.limitPassed = true;
        }
    }
}
</script>

<style scoped>
input:focus {
    outline: none;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

/* Firefox */
input[type='number'] {
    -moz-appearance: textfield;
}
</style>
