<script setup lang="ts">
import fontIcon from '../public/font.png';
import lineSpaceIcon from '../public/line-spacing.png';
import contrastThem from '../public/brightness.png';
import dyslexicFont from '../public/translation.png';
import underline from '../public/underline.png';
import { ref } from 'vue';

const fontSize = ref(2);
const lineSpacing = ref(2);

const highContrast = ref(false);
const openDyslexicFont = ref(false);
const underlineLinks = ref(false);

const font = [
    { "textSize": "Small", "fontSize": 'text-sm' },
    { "textSize": "Default", "fontSize": 'text-base' },
    { "textSize": "Large", "fontSize": 'text-lg' },
    { "textSize": "Extra Large", "fontSize": 'text-xl' },
];

const linespace = [
    { "lineSpace": "Single", "lineHeight": 'leading-[20px]' },
    { "lineSpace": "Default", "lineHeight": 'leading-[25px]' },
    { "lineSpace": "Double", "lineHeight": 'leading-[30px]' },
    { "lineSpace": "Extra-Double", "lineHeight": 'leading-[35px]' }
];


const switches = [
    {
        label: "High Contrast",
        iconSrc: contrastThem,
        modelValue: highContrast,
        switchLeft: '60',
        switchTop: '2'
    },
    {
        label: "OpenDyslexic Font",
        iconSrc: dyslexicFont,
        modelValue: openDyslexicFont,
        switchLeft: '24',
        switchTop: '2'
    },
    {
        label: "Underline Links",
        iconSrc: underline,
        modelValue: underlineLinks,
        switchLeft: '48',
        switchTop: '2'
    }
];


function fontupdate(newvalue: number) {
    fontSize.value = newvalue;
}

function lineudpate(newvalue: number){
    lineSpacing.value = newvalue;
}
</script>

<template>
    <div class="p-6">
        <h1 class="text-5xl font-bold text-[#2D2D2D] w-fit" aria-label="setting page">Settings</h1>
        <p class="text-[#6B6B6B] mt-2 w-fit">Update and change details about your account</p>

        <div class="flex space-x-6 mt-6 pb-4">
            <button class="text-[#6B6B6B]" disabled>Profile</button>
            <button class="text-[#6B6B6B]" disabled>Password</button>
            <button class="text-white bg-[#B3AEA7] px-4 py-1 rounded-lg" disabled>Accessibility</button>
            <button class="text-[#6B6B6B]" disabled>Billing</button>
        </div>
        <hr>
        <div class="bg-white mt-6 pl-9 p-6 rounded-lg shadow-sm w-6xl relative">
            <h2 class="text-xl font-bold text-[#2D2D2D]">Accessibility</h2>

            <Slider 
                heading="Font Size"
                :icon="fontIcon"
                :currentValue="2"
                ariaDecreaseButton="decrease button"
                ariaIncreaseButton="increase button"
                @updateValue="fontupdate"
                :currnetSize="font[fontSize-1].textSize"
            />

            <Slider 
                heading="Line Height"
                :icon="lineSpaceIcon"
                :currentValue="2"
                ariaDecreaseButton="decrease button"
                ariaIncreaseButton="increase button"
                @updateValue="lineudpate"
                :currnetSize="linespace[lineSpacing-1].lineSpace"
            />

            <Switch
                v-for="(item, index) in switches"
                :key="index"
                :label="item.label"
                :iconSrc="item.iconSrc"
                v-model="item.modelValue.value"
                :switchLeft="item.switchLeft"
                :switchTop="item.switchTop"
            />

            <div class="mt-3 border p-3 w-fit h-fit absolute right-0 rounded-lg top-[28%] mr-6"
                :class="{ 'dyslexic-text': openDyslexicFont }" aria-hidden="true">

                <h3 class="text-lg font-semibold">
                    Here's a page header style
                </h3>

                <p class="mt-2 mb-2 text-[#6B6B6B]" :class="font[fontSize-1].fontSize, linespace[lineSpacing-1].lineHeight">
                    Check it out! Here's an example body paragraph. Toggle <br />
                    the font size to make this text larger or smaller. Saving <br />
                    these changes will update the text across the entire <br />
                    app.
                </p>

                <a href="#" class="text-xs font-normal text-[#D16A3B]" :class="{ 'underline': underlineLinks }"
                    tabindex="-1">
                    Link to resources
                </a>
                <br />

                <div class="flex justify-end items-end mt-4 gap-2">
                    <button class="p-2 cursor-pointer" :class="{ 'underline': underlineLinks }" tabindex="-1" disabled>
                        Button 1
                    </button>

                    <button class="border cursor-pointer p-2 text-medium rounded-lg" :class="{
                        'underline': underlineLinks,
                        'bg-gray-900 text-white': highContrast,
                        'bg-[#D16A3B] text-white': !highContrast
                    }" tabindex="-1" disabled>
                        Button 2
                    </button>
                </div>
            </div>

            <div class="mt-6 flex justify-between items-end" aria-hidden="true">
                <label class="ml-auto relative mb-[9px] text-[#6B6B6B] hover:cursor-pointer">More Details</label>
                <img src="../public/maximize.png" class="h-[24px] w-[24px] cursor-pointer mb-2 ml-1" alt="">
                <div aria-hidden="true">
                    <button class="border rounded-xl p-2 ml-2 hover:cursor-pointer" disabled>Reset
                        Default
                        Settings</button>
                    <button class="border rounded-xl p-2 ml-2 bg-[#D16A3B] text-[white] hover:cursor-pointer" 
                        disabled>Apply Settings
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>