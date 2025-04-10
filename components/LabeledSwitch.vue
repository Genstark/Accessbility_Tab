<script setup lang="ts">
defineProps({
    label: String,
    iconUrl: String,
    modelValue: Boolean,
});
defineEmits(["update:modelValue"]);
</script>

<template>
    <div class="flex items-center justify-between w-full max-w-xs mt-8">
        <!-- Left: Icon + Label -->
        <div class="flex items-center gap-4">
            <img :src="iconUrl" class="h-7 w-7" alt="" />
            <span class="font-semibold">{{ label }}</span>
        </div>

        <!-- Right: Toggle with I / O -->
        <div class="inline-flex items-center cursor-pointer">
            <input type="checkbox" class="sr-only peer" :checked="modelValue"
                @change="(e) => $emit('update:modelValue', (e.target as HTMLInputElement).checked)" />
            <div class="relative w-11 h-6 bg-gray-500 rounded-full peer dark:bg-gray-700
                after:content-[''] after:absolute after:top-[2px] after:start-[2px]
                after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5
                after:transition-all peer-checked:after:translate-x-full peer-checked:after:border-white
                peer-focus-visible:outline peer-focus-visible:outline-2 peer-focus-visible:outline-black
                peer-checked:bg-[#D16A3B] dark:peer-checked:bg-[#D16A3B]">
                <span v-if="modelValue" class="absolute left-[7px] top-[2px] text-white text-sm font-semibold">I</span>
                <span v-else class="absolute right-[7px] top-[2px] text-white text-sm font-semibold">O</span>
            </div>
        </div>
    </div>
</template>
