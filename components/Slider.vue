<script setup>
defineProps({
    msg: String,
    image: String,
    textSize: String,
    decreaseButton: Function,
    increaseButton: Function,
    changeFontSize: Function,
    fontValue: Number,
    ariaDecreaseButton: String,
    ariaIncreaseButton: String
});
</script>

<template>
    <div class="mt-5">
        <div class="flex items-center">
            <img :src="image" class="w-[24px] h-[24px]" alt="">
            <label class="font-semibold ml-2">{{ msg }}:
                <span class="text-[#6B6B6B] font-normal">{{ textSize }}</span>
            </label>
        </div>

        <div class="flex items-center mt-4 justify-between border-[#dedede] rounded-xl w-72 bg-[#f8faf7] h-[60px]">
            <button class="text-4xl cursor-pointer rounded-xl negativeButton hover:bg-gray-200" 
                style="height: 100%; box-sizing: border-box; padding-bottom: 9px;
                width: 59px; margin-right: 5px;" 
                @click="decreaseButton"
                :aria-label="ariaDecreaseButton"
                role="button"
            >-
            </button>

            <div class="relative w-full">
                <hr class="absolute top-1/2 left-0 w-full border-gray-400 transform -translate-y-1/2" />
                <input type="range" min="1" max="4" step="1" :value="fontValue" @input="changeFontSize"
                    class="w-full appearance-none bg-transparent z-10 relative range-slider"
                    :aria-valuetext="textSize" 
                />
                <div class="flex justify-between absolute top-1/2 w-full transform -translate-y-1/2">
                    <span class="w-2 h-2 bg-gray-400 rounded-full"></span>
                    <span class="w-2 h-2 bg-gray-400 rounded-full"></span>
                    <span class="w-2 h-2 bg-gray-400 rounded-full"></span>
                    <span class="w-2 h-2 bg-gray-400 rounded-full"></span>
                </div>
            </div>

            <button class="text-4xl cursor-pointer rounded-xl hover:bg-gray-200" 
                style="height: 100%; box-sizing: border-box; padding-bottom: 9px;
                width: 59px; margin-left: 5px;" 
                @click="increaseButton"
                :aria-label="ariaIncreaseButton"
                role="button"
            >+
            </button>
        </div>
    </div>
</template>


<style scoped>
/* input[type="range"]::-webkit-slider-thumb {
    appearance: none;
    width: 14px;
    height: 14px;
    background-color: #D16A3B;
    border-radius: 50%;
    cursor: pointer;
    position: relative;
} */

/* .negativeButton {
    height: 100%;
    box-sizing: border-box;
    padding-bottom: 9px;
    width: 59px;
    margin-right: 5px;
} */

/* .positiveButton {
    height: 100%;
    box-sizing: border-box;
    padding-bottom: 9px;
    width: 59px;
    margin-left: 5px;
} */
</style>