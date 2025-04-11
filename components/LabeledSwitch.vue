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
        <!-- Left Side: Icon + Label -->
        <div class="flex items-center gap-4">
            <img :src="iconUrl" class="h-7 w-7" alt="icon" />
            <span class="font-semibold">{{ label }}</span>
        </div>

        <!-- Right Side: Switch with I / O indicators -->
        <div class="inline-flex items-center cursor-pointer relative">
            <!-- Show "I" when true -->
            <span v-if="modelValue"
                class="absolute left-[7px] top-[2px] text-white text-sm font-semibold pointer-events-none select-none z-10">
                I
            </span>

            <!-- Switch itself -->
            <Switch :model-value="modelValue" @update:modelValue="(val) => emit('update:modelValue', val)"
                style="width: 45px; height: 25px;" />

            <!-- Show "O" when false -->
            <span v-if="!modelValue"
                class="absolute right-[7px] top-[2px] text-white text-sm font-semibold pointer-events-none select-none z-10">
                O
            </span>
        </div>
    </div>
</template>

<style scoped>
/* Switch background colors */
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
