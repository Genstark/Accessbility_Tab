<script setup lang="ts">
defineProps<{
    label: string
    iconUrl: string
    modelValue: boolean
}>()

const emit = defineEmits<{
    (e: 'update:modelValue', value: boolean): void
}>()
</script>

<template>
    <div class="flex items-center justify-between w-full max-w-xs mt-8">
        <div class="flex items-center gap-4">
            <img :src="iconUrl" class="h-7 w-7" alt="icon" />
            <span class="font-semibold">{{ label }}</span>
        </div>
        <div class="inline-flex items-center cursor-pointer relative">
            <span v-if="modelValue"
                class="absolute left-[7px] top-[2px] text-white text-sm font-semibold pointer-events-none select-none z-10">
                I
            </span>
            <Switch :model-value="modelValue" @update:modelValue="(val) => emit('update:modelValue', val)" class="hover:cursor-pointer"
                style="width: 45px; height: 25px;" />
            <span v-if="!modelValue"
                class="absolute right-[7px] top-[2px] text-white text-sm font-semibold pointer-events-none select-none z-10">
                O
            </span>
        </div>
    </div>
</template>

<style scoped>
:deep(button[data-state="checked"]) {
    background-color: #D16A3B;
    /* Orange when on */
}

:deep(button[data-state="unchecked"]) {
    background-color: rgb(107 114 128) !important;
    /* Gray when off */
}

/* Thumb (circle) sizing */
:deep(span[data-slot="switch-thumb"]) {
    height: 20px;
    width: 20px;
}

/* Thumb positioning */
:deep(span[data-state="unchecked"]) {
    --tw-translate-x: 2px;
}

:deep(span[data-state="checked"]) {
    --tw-translate-x: calc(100% - -2px);
}
</style>
