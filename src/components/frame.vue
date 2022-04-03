<script lang="ts" setup>
import { ref, onMounted, watch } from 'vue';
const props = defineProps({
    src: {
        type: String,
        default: ''
    }
});
const frame = ref();
const isLoading = ref(true);
const load = () => {
    isLoading.value = false;
};
watch(
    () => props.src,
    () => {
        isLoading.value = true;
    },
    {
        immediate: true
    }
);
onMounted(() => {
    frame.value.onload = load;
});
</script>
<template>
    <div class="box">
        <div :class="['loading', { show: isLoading }]">
            <div class="icon">Loading Frame</div>
        </div>
        <iframe class="frame" v-if="src" :src="src" frameborder="0" ref="frame"></iframe>
    </div>
</template>
<style>
.box {
    height: 100%;
    flex: 1;
    position: relative;
}
.frame {
    height: 100%;
    width: 100%;
}
.loading {
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    background: #000;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 36px;
    transition: all 0.5s;
    opacity: 0;
    z-index: -1;
}
.show {
    z-index: 2;
    opacity: 1;
}
.icon {
    position: relative;
    width: 300px;
    height: 300px;
    display: flex;
    align-items: center;
    justify-content: center;
    --colorA: #b78eff;
}
.icon::before,
.icon::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    border-radius: 50%;
    border-top: 10px solid #fff;
    filter: drop-shadow(0 0 2px var(--colorA)) drop-shadow(0 0 5px var(--colorA))
        drop-shadow(0 0 10px var(--colorA)) drop-shadow(0 0 20px var(--colorA));
    animation: rotate 3s infinite linear;
}

.icon::after {
    --colorA: #ffec41;
    animation-delay: -1.5s;
}

@keyframes rotate {
    100% {
        transform: rotate(360deg);
    }
}
</style>
