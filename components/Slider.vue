<script setup lang="ts">
const props = defineProps({
    label: String,
    iconUrl: String,
    value: Number,
    displayText: String
});

const emit = defineEmits(['updateValue']);
const changeValue = ref(props.value || 2);

function handleThumbClick(event: number) { // Renamed function
    changeValue.value = event;
    emit('updateValue', changeValue.value);
}

function decreaseButton() {
    if (changeValue.value > 1) {
        changeValue.value--;
        emit('updateValue', changeValue.value);
    }
}

function increaseButton() {
    if (changeValue.value < 4) {
        changeValue.value++;
        emit('updateValue', changeValue.value);
    }
}
</script>

<template>
    <div class="mt-5">
        <div class="flex items-center">
            <img :src="iconUrl" class="w-[24px] h-[24px]" alt="">
            <label class="font-semibold ml-2">{{ label }}:
                <span class="text-[#6B6B6B] font-normal">{{ displayText }}</span>
            </label>
        </div>

        <div class="flex items-center mt-4 justify-between border-[#dedede] rounded-xl w-72 bg-[#f8faf7] h-[60px]">
            <button class="text-4xl cursor-pointer rounded-xl hover:bg-gray-200" 
                style="height: 100%; box-sizing: border-box; padding-bottom: 9px;
                width: 59px; margin-right: 5px;" 
                @click="decreaseButton"
                aria-label="decrease button"
                role="button"
            >-
            </button>

            <div class="relative w-full">
                <hr class="absolute top-1/2 left-0 w-full border-gray-400 transform -translate-y-1/2" />
                <input type="range" min="1" max="4" step="1" v-model="changeValue"
                    class="w-full appearance-none bg-transparent z-10 relative range-slider pointer-events-none"
                    :aria-valuetext="displayText" 
                />
                <div class="flex justify-between absolute top-1/2 w-full transform -translate-y-1/2 z-0">
                    <span
                        v-for="index in 4"
                        :key="index"
                        class="w-2 h-2 bg-gray-400 rounded-full pointer-events-auto cursor-pointer"
                        @click="handleThumbClick(index)"
                    ></span>
                </div>
            </div>

            <button class="text-4xl cursor-pointer rounded-xl hover:bg-gray-200" 
                style="height: 100%; box-sizing: border-box; padding-bottom: 9px;
                width: 59px; margin-left: 5px;" 
                @click="increaseButton"
                aria-label="increase button"
                role="button"
            >+
            </button>
        </div>
    </div>
</template>