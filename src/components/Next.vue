<script setup lang="ts">
interface IState {
    msg: string;
}
import {reactive} from 'vue';
const state: IState = reactive({
    msg: 'Hello Next'
});
</script>

<template>
    <div class="msg">
        {{ state.msg }}
    </div>
</template>

<style scoped>
.msg {
    color: red;
}
</style>