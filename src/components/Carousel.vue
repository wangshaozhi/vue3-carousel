<script setup lang="ts">
import {reactive, onMounted, toRefs, defineProps} from 'vue';

const state: {imageList: string[]} = reactive({
    imageList: [
    'https://p6.qhimg.com/bdr/__85/t01384e4540636d2f40.jpg',
    'https://p6.qhimg.com/bdr/__85/t017999da786a85433b.jpg',
    'https://p0.qhimg.com/bdr/__85/t01bfba0fc70ae2812f.jpg'
]
});

const {imageList} = toRefs(state);

onMounted(() => {
    const firstImage = state.imageList[0];
    const lastImage = state.imageList[state.imageList.length - 1];
    state.imageList = [lastImage, ...state.imageList, firstImage];
    console.log('mounted')
    console.log(imageList)
});

defineProps<{msg: string}>()
</script>

<template>
    <h2>{{ msg }}</h2>
    <div class="carousel-wrapper">
        <div>
            <div v-for="item in imageList" :key="item">
                <img
                    :src="item"
                    class="image"
                />
            </div>
        </div>
        <div class="indicator-wrapper">
            <div v-for="url in imageList" :key="url">
                <span>{{url}}</span>
            </div>
        </div>
    </div>
</template>

<style scoped>
.image {
    width: 100%;
}
</style>