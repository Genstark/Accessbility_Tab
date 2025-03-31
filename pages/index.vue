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
                msg="Font Size" 
                :image="fontIcon" 
                :textSize="fontSizeChecker().textSize"
                :decreaseButton="decreaseFontSize" 
                :increaseButton="increaseFontSize" 
                :changeFontSize="updateFontSize"
                :fontValue="fontSize" 
                ariaDecreaseButton="decrease font size"
                ariaIncreaseButton="increase font size"
            />

            <Slider
                msg="Line Space"
                :image="lineSpaceIcon"
                :textSize="lineSpacingChecker().lineSpace"
                :decreaseButton="decreaseLineSpacing" 
                :increaseButton="increaseLineSpacing" 
                :changeFontSize="updateLineSpacing"
                :fontValue="lineSpacing"
                ariaDecreaseButton="decrease line space"
                ariaIncreaseButton="increase line space"
            />

            <Switch
                label="High Contrast"
                :iconSrc="contrastThem"
                v-model="highContrast"
                switchLeft="60"
                switchTop="2"
            />

            <!-- <div class="mt-12">
                <label class="inline-flex items-center cursor-pointer" id="highContrastLabel">
                    <img src="../public/brightness.png" class="h-[24px] w-[24px]" alt="">
                    <span class="font-semibold ml-[10px]">High Contrast</span>
                    <input type="checkbox" value="" class="sr-only peer" v-model="highContrast" id="highContrastToggle"
                        aria-labelledby="highContrastLabel">
                    <div
                        class="relative left-[60px] top-[2px] w-11 h-6 bg-gray-200 
                        peer-focus-visible:outline peer-focus-visible:outline-2 peer-focus-visible:outline-[#000000] 
                        dark:peer-focus-visible:outline-[#000000] 
                        rounded-full peer dark:bg-gray-700 
                        peer-checked:after:translate-x-full rtl:peer-checked:after:-translate-x-full 
                        peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:start-[2px] 
                        after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5
                        after:transition-all dark:border-gray-600 peer-checked:bg-[#D16A3B] dark:peer-checked:bg-[#D16A3B]">
                        <span aria-hidden="true" class="relative left-[8px] bottom-[1px] text-[white]"
                            v-if="highContrast">I</span>
                        <span aria-hidden="true" class="relative left-[26px] bottom-[1px] text-[white]"
                            v-if="!highContrast">O</span>
                    </div>
                </label>
            </div> -->

            <Switch
                label="OpenDyslexic Font"
                :iconSrc="dyslexicFont"
                v-model="openDyslexicFont"
                switchLeft="24"
                switchTop="2"
            />

            <!-- <div class="mt-12">
                <label class="inline-flex items-center cursor-pointer">
                    <img src="../public/translation.png" class="h-[24px] w-[24px]" alt="">
                    <span class="font-semibold ml-[10px]">OpenDyslexic Font</span>
                    <input type="checkbox" value="" class="sr-only peer" v-model="openDyslexicFont" />
                    <div
                        class="relative left-[24px] top-[2px] w-11 h-6 bg-gray-200
                        peer-focus-visible:outline peer-focus-visible:outline-2 peer-focus-visible:outline-[#000000] 
                        dark:peer-focus-visible:outline-[#000000] 
                        rounded-full peer dark:bg-gray-700 
                        peer-checked:after:translate-x-full rtl:peer-checked:after:-translate-x-full 
                        peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:start-[2px] 
                        after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5
                        after:transition-all dark:border-gray-600 peer-checked:bg-[#D16A3B] dark:peer-checked:bg-[#D16A3B]">
                        <span aria-hidden="true" class="relative left-[8px] bottom-[1px] text-[white]"
                            v-if="openDyslexicFont">I</span>
                        <span aria-hidden="true" class="relative left-[26px] bottom-[1px] text-[white]"
                            v-if="!openDyslexicFont">O</span>
                    </div>
                </label>
            </div> -->

            <Switch
                label="Underline Links"
                :iconSrc="underline"
                v-model="underlineLinks"
                switchLeft="48"
                switchTop="2"
            />

            <!-- <div class="mt-12">
                <label class="inline-flex items-center cursor-pointer">
                    <img src="../public/underline.png" class="h-[24px] w-[24px]" alt="">
                    <span class="font-semibold ml-[10px]">Underline Links</span>
                    <input type="checkbox" value="" class="sr-only peer" v-model="underlineLinks" />
                    <div
                        class="relative left-[48px] top-[2px] w-11 h-6 bg-gray-200
                        peer-focus-visible:outline peer-focus-visible:outline-2 peer-focus-visible:outline-[#000000] 
                        dark:peer-focus-visible:outline-[#000000] 
                        rounded-full peer dark:bg-gray-700 
                        peer-checked:after:translate-x-full rtl:peer-checked:after:-translate-x-full 
                        peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:start-[2px] 
                        after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5
                        after:transition-all dark:border-gray-600 peer-checked:bg-[#D16A3B] dark:peer-checked:bg-[#D16A3B]">
                        <span aria-hidden="true" class="relative left-[8px] bottom-[1px] text-[white]"
                            v-if="underlineLinks">I</span>
                        <span aria-hidden="true" class="relative left-[26px] bottom-[1px] text-[white]"
                            v-if="!underlineLinks">O</span>
                    </div>
                </label>
            </div> -->

            <div class="mt-3 border p-3 w-fit h-fit absolute right-0 rounded-lg top-[28%] mr-6"
                :class="{ 'dyslexic-text': openDyslexicFont }" aria-hidden="true">

                <h3 class="text-lg font-semibold">
                    Here's a page header style
                </h3>

                <p class="mt-2 mb-2 text-[#6B6B6B]" :class="fontSizeChecker().fontSize,
                    lineSpacingChecker().lineHeight
                    ">
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
                    <button class="border rounded-xl p-2 ml-2 hover:cursor-pointer" @click="resetButton" disabled>Reset
                        Default
                        Settings</button>
                    <button class="border rounded-xl p-2 ml-2 bg-[#D16A3B] text-[white] hover:cursor-pointer" disabled
                        @click="settingChangeMessage">Apply Settings</button>
                </div>
            </div>
        </div>
    </div>
</template>

<!-- 
relative left-[9px] top-[2px] w-11 h-6 peer-checked:bg-[#D16A3B] rounded-full border border-gray-400 
peer peer-focus:ring-0 dark:peer-checked:bg-[#D16A3B] peer-checked:after:translate-x-full 
rtl:peer-checked:after:-translate-x-full after:absolute after:top-0.5 after:start-[2px] after:text-black
peer-checked:after:text-white after:flex after:items-center after:justify-center after:border-gray-400
after:border after:rounded-full after:h-5 after:w-5 after:transition-all dark:border-gray-600

<span class="relative left-[6px] bottom-[1px]" v-if="highContrast">I</span>
<span class="relative left-[26px] bottom-[1px]" v-if="!highContrast">O</span>
 -->

<script setup>
import fontIcon from '../public/font.png';
import lineSpaceIcon from '../public/line-spacing.png';
import contrastThem from '../public/brightness.png';
import dyslexicFont from '../public/translation.png';
import underline from '../public/underline.png';
import { ref, watch } from 'vue';

const fontSize = ref(2);
const lineSpacing = ref(2);

const highContrast = ref(false);
const openDyslexicFont = ref(false);
const underlineLinks = ref(false);
let changes = false;

watch([highContrast, openDyslexicFont, underlineLinks, fontSize, lineSpacing], (newValue) => {
    console.log('toggle is working');
    changes = true;
});

function settingChangeMessage() {
    // console.log('settings changed');
    if (changes === true) {
        alert('Your Default setting is change');
    }
    else {
        alert('No changes made');
    }
}

function resetButton() {
    fontSize.value = 2;
    lineSpacing.value = 2;
    highContrast.value = false;
    openDyslexicFont.value = false;
    underlineLinks.value = false;
    changes = false;
}

const updateFontSize = (event) => {
    fontSize.value = event.target.value;
};

const updateLineSpacing = (event) => {
    lineSpacing.value = event.target.value;
};

const fontSizeChecker = () => {
    if (fontSize.value == 1) {
        return { "textSize": "Small", "fontSize": 'text-sm' };
    }
    else if (fontSize.value == 2) {
        return { "textSize": "Default", "fontSize": 'text-base' };
    }
    else if (fontSize.value == 3) {
        return { "textSize": "Large", "fontSize": 'text-lg' };
    }
    else {
        return { "textSize": "Extra-Large", "fontSize": 'text-xl' };
    }
};

const lineSpacingChecker = () => {
    if (lineSpacing.value == 1) {
        return { "lineSpace": "Single", "lineHeight": 'leading-[20px]' };
    }
    else if (lineSpacing.value == 2) {
        return { "lineSpace": "Default", "lineHeight": 'leading-[25px]' };
    }
    else if (lineSpacing.value == 3) {
        return { "lineSpace": "Double", "lineHeight": 'leading-[30px]' };
    }
    else {
        return { "lineSpace": "Extra-Double", "lineHeight": 'leading-[35px]' };
    }
};

const decreaseFontSize = () => {
    if (fontSize.value > 1) {
        fontSize.value--;
    }
};

const increaseFontSize = () => {
    if (fontSize.value < 4) {
        fontSize.value++;
    }
};

const decreaseLineSpacing = () => {
    if (lineSpacing.value > 1) {
        lineSpacing.value--;
    }
};

const increaseLineSpacing = () => {
    if (lineSpacing.value < 4) {
        lineSpacing.value++;
    }
};
</script>

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

/* 
.negativeButton {
    height: 100%;
    box-sizing: border-box;
    padding-bottom: 9px;
    width: 59px;
    margin-right: 5px;
}

.positiveButton {
    height: 100%;
    box-sizing: border-box;
    padding-bottom: 9px;
    width: 59px;
    margin-left: 5px;
} */

/* 
    position: relative;
    bottom: 3px;
    right: 3px; 
*/
</style>