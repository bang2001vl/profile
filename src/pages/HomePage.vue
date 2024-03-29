<template>
    <div class="page home">
        <TextWave class="title" text="BangNPD">
            <h1>BangNPD</h1>
        </TextWave>
        <LiquidBackground style="width: 100%; height: 70px;"></LiquidBackground>
    </div>
</template>

<script setup lang="ts">
import LiquidBackground from '../components/LiquidBackground.vue';
import TextWave from '../components/TextWave.vue';
</script>

<style>
.page.home {
    & .title {
        width: 100%;
        height: 200px;
        font-family: Anton;
    }
}
</style>
