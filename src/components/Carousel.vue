<script setup lang="ts">
import {reactive, onMounted, toRefs, defineProps, CSSProperties, computed} from 'vue';
interface IState {
    imageList: string[];
    imageWrapperStyle: CSSProperties;
};

const state: IState = reactive({
    imageList: [
        'https://p6.qhimg.com/bdr/__85/t01384e4540636d2f40.jpg',
        'https://p6.qhimg.com/bdr/__85/t017999da786a85433b.jpg',
        'https://p0.qhimg.com/bdr/__85/t01bfba0fc70ae2812f.jpg'
    ],
    imageWrapperStyle: {background: 'red'}
});
const {imageList} = toRefs(state);

onMounted(() => {
    /**
     * 初始化图片列表
     */
    const initImageList = () => {
        const firstImage = state.imageList[0];
        const lastImage = state.imageList[state.imageList.length - 1];
        state.imageList = [lastImage, ...state.imageList, firstImage];
    };
    
    initImageList();
});

const onDotClick = (index: number) => {
    state.imageWrapperStyle = {
        transform: `translateX(${-100 * index})%`
    };
};

defineProps<{msg: string}>();

</script>

<template>
    <h2>{{ msg }}</h2>
    <div class="carousel-wrapper">
        <div
            class="image-wrapper"
            :style="state.imageWrapperStyle"
        >
            <img
                v-for="item in imageList"
                :key="item"
                :src="item"
                class="image"
            />
        </div>
        <div class="indicator-wrapper">
            <span
                v-for="idx in imageList.map((_, index) => index)"
                :key="idx"
                class="dot"
                @click="() => onDotClick(idx)"
            >
            </span>
        </div>
        {{ state.imageWrapperStyle }}
    </div>
</template>

<style scoped>

.carousel-wrapper {
    position: relative;
    width: 500px;
}

.image-wrapper {
    display: flex;
}

.image {
    width: 500px;
}

.indicator-wrapper {
    position: absolute;
    bottom: 20px;
    left: 50%;
    display: flex;
    transform: translateX(-50%);
}

.dot {
    width: 20px;
    height: 20px;
    margin-right: 8px;
    border-radius: 50%;
    border: 1px solid #ccc;
    cursor: pointer;
}
</style>