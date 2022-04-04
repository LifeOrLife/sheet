<script setup lang="ts">
import { ref, reactive } from 'vue';
import frame from './components/frame.vue';

type Item = {
    src: string;
    name: string;
};

const list = reactive([
    { src: 'https://xiaolincoding.com', name: '图解网络' },
    { src: 'https://cheatsheet.wang/', name: 'git' },
    { src: 'https://visualgo.net/en', name: '算法演示' },
    { src: 'https://regex-vis.com/', name: '正则表达式匹配效果' },
    { src: 'https://pattern.windliang.wang', name: '前端设计模式' },
    { src: 'https://yqnn.github.io/svg-path-editor/', name: 'svg在线编辑' },
    { src: 'https://interview2.poetries.top/docs/base.html', name: '前端面试指南' },
    { src: 'https://learngitbranching.js.org/?locale=zh_CN', name: 'Learn Git Branching' }
]);
const active = ref(list[0].src);
const switchActive = (item: Item) => {
    active.value = item.src;
};
</script>

<template>
    <main>
        <nav>
            <div
                :class="['item', { active: item.src === active }]"
                @click="switchActive(item)"
                v-for="item in list"
            >
                {{ item.name }}
            </div>
        </nav>
        <frame :src="active" />
    </main>
</template>

<style>
@import './assets/base.css';
html,
body {
    height: 100%;
}
#app {
    height: 100%;
    font-weight: normal;
}
nav {
    height: 100%;
    width: 200px;
    box-shadow: 0 0 5px 5px rgba(0, 0, 0, 0.09);
    position: relative;
    z-index: 1;
}
.item {
    height: 30px;
    display: flex;
    align-items: center;
    padding: 0 10px;
    text-overflow: ellipsis;
    white-space: nowrap;
    cursor: pointer;
    transition: background 0.5s;
}
.item:hover {
    background: rgb(222, 238, 247);
}
.item.active {
    color: #6cf;
}
main {
    height: 100%;
    display: flex;
    overflow: hidden;
}
</style>
