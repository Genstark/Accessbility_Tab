<script setup lang="ts">
defineProps({
    label: String, // Label for the toggle
    iconUrl: String, // Icon image source
    modelValue: Boolean,
    switchLeft: String, // Left position of the toggle
    switchTop: String // Top position of the toggle
});
defineEmits(["update:modelValue"]); // Required to update the parent state  
</script>

<template>
    <div class="mt-12">
        <label class="inline-flex items-center cursor-pointer">
            <img :src="iconUrl" class="h-[24px] w-[24px]" alt="" />
            <span class="font-semibold ml-[10px]">{{ label }}</span>
            <input type="checkbox" class="sr-only peer" :checked="modelValue"
                @change="(event) => $emit('update:modelValue', (event.target as HTMLInputElement).checked)" />
            <div class="relative transition-all w-11 h-6 bg-gray-200 
                peer-focus-visible:outline peer-focus-visible:outline-2 peer-focus-visible:outline-[#000000] 
                dark:peer-focus-visible:outline-[#000000] 
                rounded-full peer dark:bg-gray-700 
                peer-checked:after:translate-x-full rtl:peer-checked:after:-translate-x-full 
                peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:start-[2px] 
                after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5
                after:transition-all dark:border-gray-600 peer-checked:bg-[#D16A3B] dark:peer-checked:bg-[#D16A3B]"
                :style="{ left: switchLeft + 'px', top: switchTop + 'px' }"
            >
                <span aria-hidden="true" class="relative left-[8px] bottom-[1px] text-[white]"
                    v-if="modelValue">I</span>
                <span aria-hidden="true" class="relative left-[26px] bottom-[1px] text-[white]"
                    v-if="!modelValue">O</span>
            </div>
        </label>
    </div>
</template>