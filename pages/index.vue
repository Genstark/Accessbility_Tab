<script setup lang="ts">
import fontIcon from '../public/font.png';
import lineSpaceIcon from '../public/line-spacing.png';
import contrastThem from '../public/brightness.png';
import dyslexicFont from '../public/translation.png';
import underline from '../public/underline.png';
import json from '../public/config.json';
import { ref } from 'vue';
import LabeledSwitch from '~/components/LabeledSwitch.vue';

const selectedFontSize = ref(2);
const selectedLineSpacing = ref(2);

const isHighContrast = ref(false);
const useDyslexicFont = ref(false);
const showUnderlinedLinks = ref(false);


const switches = [
    {
        label: "High Contrast",
        iconSrc: contrastThem,
        modelValue: isHighContrast
    },
    {
        label: "OpenDyslexic Font",
        iconSrc: dyslexicFont,
        modelValue: useDyslexicFont
    },
    {
        label: "Underline Links",
        iconSrc: underline,
        modelValue: showUnderlinedLinks
    }
];


function fontupdate(newvalue: number) {
    selectedFontSize.value = newvalue;
}

function lineudpate(newvalue: number){
    selectedLineSpacing.value = newvalue;
}

const checked = ref(false);

watch(checked, (newvalue) => {
    console.log(newvalue);
});
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
                label="Font Size"
                :iconUrl="fontIcon"
                :currentValue="2"
                @updateValue="fontupdate"
                :currnetSize="json.fontSize[selectedFontSize-1].text"
            />

            <Slider 
                label="Line Height"
                :iconUrl="lineSpaceIcon"
                :currentValue="2"
                @updateValue="lineudpate"
                :currnetSize="json.lineHeight[selectedLineSpacing-1].text"
            />

            <LabeledSwitch
                v-for="(item, index) in switches"
                :key="index"
                :label="item.label"
                :iconUrl="item.iconSrc"
                v-model="item.modelValue.value"
            />

            <div class="mt-3 border p-3 w-fit h-fit absolute right-0 rounded-lg top-[28%] mr-6"
                :class="{ 'dyslexic-text': useDyslexicFont }" aria-hidden="true">

                <h3 class="text-lg font-semibold">
                    Here's a page header style
                </h3>

                <p class="mt-2 mb-2 text-[#6B6B6B]" :class="json.fontSize[selectedFontSize-1].class, json.lineHeight[selectedLineSpacing-1].class">
                    Check it out! Here's an example body paragraph. Toggle <br />
                    the font size to make this text larger or smaller. Saving <br />
                    these changes will update the text across the entire <br />
                    app.
                </p>

                <a href="#" class="text-xs font-normal text-[#D16A3B]" :class="{ 'underline': showUnderlinedLinks }"
                    tabindex="-1">
                    Link to resources
                </a>
                <br />

                <div class="flex justify-end items-end mt-4 gap-2">
                    <button class="p-2 cursor-pointer font-meduim" :class="{ 'underline': showUnderlinedLinks }" tabindex="-1" disabled>
                        Button 1
                    </button>

                    <Button size="lg" class="bg-[#D16A3B] hover:bg-[none] hover:cursor-pointer font-meduim text-[white] rounded-lg"
                        :class="{
                            'underline': showUnderlinedLinks,
                            'bg-gray-900 text-white': isHighContrast,
                            'bg-[#D16A3B] text-white': !isHighContrast
                        }" tabindex="-1">Button 2
                    </Button>
                </div>
            </div>

            <div class="mt-6 flex justify-between items-end" aria-hidden="true">
                <label class="ml-auto relative mb-[7px] text-[#6B6B6B] hover:cursor-pointer">More Details</label>
                <img src="../public/maximize.png" class="h-[22px] w-[22px] cursor-pointer mb-2 ml-1" alt="">
                <div aria-hidden="true">
                    <Button class="border rounded-xl p-2 ml-2 hover:cursor-pointer text-[#6B6B6B] bg-[white] hover:bg-[none]">
                        Reset Default Settings
                    </Button>
                    <Button class="border rounded-xl p-2 ml-2 bg-[#D16A3B] text-[white] hover:cursor-pointer hover:bg-[none]">
                        Apply Settings
                    </Button>
                </div>
            </div>
        </div>
        <!-- <div>
            <span v-if="checked" class="relative bottom-[5px] left-[13px] text-sm font-semibold text-[white] pointer-events-none select-none">I</span>
            <Switch style="width: 45px; height: 25px;" v-model="checked" />
            <span v-if="!checked" class="relative bottom-[5px] right-[16px] text-sm font-semibold text-[white] pointer-events-none select-none">O</span>
        </div> -->
    </div>
</template>

<style scoped>
/* button[role="switch"] span[data-slot="switch-thumb"] {
    background-color: aquamarine !important;
} */
/* :deep(button[data-state="checked"]){
    background-color: #D16A3B;
}
:deep(button[data-state="unchecked"]){
    background-color: rgb(107 114 128) !important;
}
:deep(span[data-slot="switch-thumb"]) {
    height: 20px;
    width: 20px;
}
:deep(span[data-state="unchecked"]){
    --tw-translate-x: 2px;
}
:deep(span[data-state="checked"]) {
    --tw-translate-x: calc(100% - -2px);
} */
</style>