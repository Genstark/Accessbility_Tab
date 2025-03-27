<script setup>
import { ref } from 'vue';
const count = ref(0);
</script>

<template>
    <div class="slider-container">
        <input type="range" min="0" max="3" step="1" value="0" id="slider">
        <div class="value" id="slider-value">0</div>
    </div>
</template>

<style lang="css" scoped>
.slider-container {
    width: 100%;
    max-width: 300px;
    margin: 50px auto;
}

input[type="range"] {
    width: 100%;
    /* -webkit-appearance: none; */
    appearance: none;
    height: 8px;
    border-radius: 5px;
    background: #ddd;
    outline: none;
    transition: background 0.3s ease;
}

input[type="range"]::-webkit-slider-runnable-track {
    width: 100%;
    height: 8px;
    background: #ddd;
    border-radius: 5px;
}

input[type="range"]::-webkit-slider-thumb {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background: #4CAF50;
    border: none;
    cursor: pointer;
    transition: background 0.3s ease;
}

input[type="range"]:focus::-webkit-slider-runnable-track {
    background: #ccc;
}

.value {
    text-align: center;
    margin-top: 10px;
    font-size: 18px;
}
</style>