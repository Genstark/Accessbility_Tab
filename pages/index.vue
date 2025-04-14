<script setup lang="ts">
import json from '../public/config.json';
import { ref } from 'vue';

const selectedFontSize = ref(2);
const selectedLineSpacing = ref(2);

const isHighContrast = ref(false);
const useDyslexicFont = ref(false);
const showUnderlinedLinks = ref(false);


const toogleValue = [
    isHighContrast,
    useDyslexicFont,
    showUnderlinedLinks
];

function fontupdate(newvalue: number) {
    selectedFontSize.value = newvalue;
}

function lineudpate(newvalue: number){
    selectedLineSpacing.value = newvalue;
}
const slidercomponentfunction = [
    fontupdate,
    lineudpate
];
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
                v-for="(item, index) in json.slider"
                :key="index"
                :label="item.label"
                :iconUrl="item.iconSrc" 
                @updateValue="slidercomponentfunction[index]"
                :displayText="index === 0 ? json.fontSize[selectedFontSize-1].text : json.lineHeight[selectedLineSpacing-1].text"
                :value="index === 0 ? selectedFontSize : selectedLineSpacing"
            />

            <LabeledSwitch
                v-for="(item, index) in json.labeledSwitch"
                :key="index"
                :label="item.label"
                :iconUrl="item.iconSrc"
                v-model="toogleValue[index].value"
            />

            <div class="mt-3 border p-3 max-w-xl max-h-lg absolute right-0 rounded-lg top-[24%] mr-6"
                :class="{ 'dyslexic-text': useDyslexicFont }" aria-hidden="true">

                <h3 class="text-lg font-semibold">
                    Here's a page header style
                </h3>

                <p class="mt-2 mb-2 text-[#6B6B6B]" :class="json.fontSize[selectedFontSize-1].class, json.lineHeight[selectedLineSpacing-1].class">
                    Check it out! Here's an example body paragraph. Toggle
                    the font size to make this text larger or smaller. Saving
                    these changes will update the text across the entire
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
                <label class="ml-auto relative mb-[9px] text-[#6B6B6B] hover:cursor-pointer">More Details</label>
                <img src="../public/maximize.png" class="h-[24px] w-[24px] cursor-pointer mb-2 ml-1" alt="">
                <div aria-hidden="true">
                    <Button
                        variant="outline"
                        size="lg"
                        class="border rounded-xl p-2 ml-2 hover:cursor-pointer"
                    >
                        Reset Default Settings
                    </Button>
                    <Button
                        variant="default"
                        size="lg"
                        class="border rounded-xl p-2 ml-2 bg-[#D16A3B] text-[white] hover:bg-[#b3542e]"
                    >
                        Apply Settings
                    </Button>
                </div>
            </div>
        </div>
    </div>
</template>