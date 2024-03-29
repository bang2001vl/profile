<template>
    <div class="text-wave container">
        <div v-for="style, index in textStyles" :key="index" class="text" :style="style">
            <slot>
                {{ 'Text' }}
            </slot>
        </div>
    </div>
</template>

<script setup lang="ts">
import { computed, type HTMLAttributes } from 'vue';

const splitCount = 26; // 130 / 5

const textStyles = computed(() => {
    const styles: HTMLAttributes['style'][] = [];
    for (let i = 0; i < splitCount; i++) {
        const param = 130 / splitCount;
        const animationLength = 2000; // In millis
        const animationDelayBetweenFirstAndLast = animationLength * 1.5; // In millis
        const animationDelayBetweenEach = - Math.round(animationDelayBetweenFirstAndLast - i * animationDelayBetweenFirstAndLast / splitCount); // In millis
        styles[i] = {
            position: "absolute",
            top: "50%",
            left: "50%",
            color: "#fff",
            padding: "20px 0",
            mixBlendMode: "screen",
            transformStyle: "preserve-3d",
            animation: `wave ${animationLength}ms ${animationDelayBetweenEach}ms ease-in-out infinite alternate`,
            clipPath: `polygon(${-30 + i * param}% 0, ${-20 + i * param}% 0, ${20 + i * param}% 100%, ${i * param}% 100%)`,
        };
    }
    return styles;
})
</script>

<style scoped lang="scss">
div {
    will-change: transform;
}

.container {
    transform-style: preserve-3d;
    position: relative;
}
</style>

<style>
@keyframes wave {
    0% {
        transform: translate(-50%, -50%) scale(0.9) rotateX(10deg) rotateY(10deg) rotateZ(0deg);
        color: rgba(0, 30, 100, 1);
    }

    100% {
        transform: translate(-50%, -50%) scale(1) rotateX(0deg) rotateY(0deg) rotateZ(0deg);
        color: rgba(50, 230, 255, 1);
    }
}
</style>