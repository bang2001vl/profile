<template>
    <div ref="container" class="container">
        <div class="content-container"></div>
        <div class="liquid">
            <div class="wave-container">
                <div v-for="index in waveNumber" :key="index" class="wave"
                    :style="{ width: `${waveSize.width}px`, height: `${waveSize.height}px` }">
                    <div class="wave-child-before"></div>
                    <div class="wave-child-after"></div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from 'vue';

const waveSize = {
    width: 100, // In pixels
    height: 100, // In pixels
}
const waveNumber = ref(1);
const container = ref<HTMLDivElement | null>(null);

const handleSizeChange = () => {
    console.log('On SizeCHanged');
    const newW = container.value!.offsetWidth;
    const newH = container.value!.offsetHeight;
    waveNumber.value = 1 + Math.ceil(newW / waveSize.width);
    console.log({ newW, newH, newVal: waveNumber.value })
}
const sizeObserver = new ResizeObserver(handleSizeChange);

onMounted(() => {
    if (container.value != null) {
        handleSizeChange()
        sizeObserver.observe(container.value);
    }
})

onBeforeUnmount(() => {
    sizeObserver.disconnect();
})
</script>

<style scoped>
.container {
    position: relative;
    width: 200px;
    height: 100px;
}

.content-container {
    width: 100px;
    height: 60px;
}

.liquid {
    z-index: -4;
    top: 0;
    left: 0;
    position: absolute;
    width: 100%;
    height: 100%;
    background: #4973ff;
    box-shadow: inset 0 0 50px rgba(0, 0, 0, .5);
    transition: cubic-bezier();
}

.wave-container {
    display: flex;
    position: absolute;
    top: 0;
    left: 0;
}

.wave {
    position: relative;
}

.wave-child-before,
.wave-child-after {
    content: '';
    top: 0;
    position: absolute;
    border-radius: 35%;
}

.wave-child-before {
    width: 190%;
    height: 190%;
    transform: translate(0%, -75%);
    background-color: white;
    animation: 7s linear infinite 0.1s spin;
}

.wave-child-after {
    width: 200%;
    height: 200%;
    transform: translate(0%, -75%);
    background-color: rgba(256, 256, 256, .5);
    animation: 7s linear infinite spin;
}

@keyframes spin {
    from {
        transform: translate(-50%, -93%) rotate(0deg);
    }

    to {
        transform: translate(-50%, -93%) rotate(360deg);
    }
}
</style>