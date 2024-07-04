<!-- Для мобильной версии будет проще сделать отдельный компонент, потому что оригинал сильно меняет структуру и я заебусь её переиначивать в адаптиве -->

<script setup>
import { inject, ref, onMounted } from 'vue'
import axios from 'axios'
import SupplementsList from './SupplementsList.vue'
import QuantityChange from '../controls/QuantityChange.vue'

const props = defineProps({
    imageUrl: String,
    itemId: Number
})

const dropdownFlag = ref(true)
const massCoefficient = ref(1)
const massCoefficientFlag = ref(false)
const quantityProduct = ref(1)

// функия изменения коэффициента массы
function changeMassCoefficient(value) {
    if (value === 1) {
        massCoefficient.value = itemsList.value[0].itemMass / 100
        massCoefficientFlag.value = true
    } else if (value === 0) {
        massCoefficient.value = 1
        massCoefficientFlag.value = false
    }
    console.log(massCoefficientFlag.value)
    console.log(value)
}

function calcNutrinicalValue(elementIndex) {
    return (
        itemsList.value[0].itemNutritionalValue[elementIndex].nutritionalValue *
        massCoefficient.value
    ).toFixed(1)
}

// Данные о продукте
const itemsList = ref([])
onMounted(async () => {
    try {
        const { data } = await axios.get(
            `https://14c3bbbcd96e00ef.mokky.dev/items-v2?itemId=${props.itemId}`
        )
        itemsList.value = data
    } catch (error) {
        console.log(error)
    }
})
const flagInvert = inject('flagInvert')
</script>

<template>
    <div class="loading option">
        <button @click="flagInvert" class="close">
            <svg
                width="20"
                height="20"
                viewBox="0 0 16 16"
                xmlns="http://www.w3.org/2000/svg"
                class=""
            >
                <path
                    fill-rule="evenodd"
                    clip-rule="evenodd"
                    d="M15.5314 0.46863C14.9065 -0.15621 13.8934 -0.15621 13.2686 0.46863L7.99999 4.93727L2.73137 0.46863C2.10653 -0.156209 1.09347 -0.156209 0.468629 0.46863C-0.108145 1.04541 -0.152512 1.95297 0.335527 2.58064L0.468629 2.73137L5.73725 8.00001L0.468629 13.2686L0.335527 13.4194C-0.152512 14.0471 -0.108145 14.9546 0.468629 15.5314C1.09347 16.1562 2.10653 16.1562 2.73137 15.5314L7.99999 10.2627L13.2686 15.5314C13.8934 16.1562 14.9065 16.1562 15.5314 15.5314C16.1081 14.9546 16.1525 14.0471 15.6644 13.4194L15.5314 13.2686L11.0627 8.00001L15.5314 2.73137L15.6644 2.58064C16.1525 1.95297 16.1081 1.04541 15.5314 0.46863Z"
                ></path>
            </svg>
        </button>
        <svg class="loading--icon" viewBox="0 0 32 35" xmlns="http://www.w3.org/2000/svg">
            <path
                fill="currentColor"
                d="M32 20.3239C31.7549 17.8723 29.3031 16.6466 27.8322 18.1176C26.8517 19.0982 26.8517 21.3046 26.3614 22.7756C25.8711 24.4918 24.4001 25.9628 23.1742 26.9434C20.2323 29.1498 15.8194 29.1498 12.142 28.4144C10.4259 27.924 8.95491 26.9434 7.72911 25.7175C4.54203 22.5305 4.54203 17.1369 6.5033 13.4594C8.21943 10.7628 11.1614 8.80144 14.3484 8.80144C14.3484 9.53693 14.3484 10.0272 14.3484 10.7627C14.3484 11.4982 14.8387 12.4788 16.0646 12.4788C17.5356 12.4788 21.9485 9.53693 23.9098 8.31114C24.4001 8.06598 24.8904 7.33051 24.6452 6.84019C24.6452 6.59503 23.9098 5.85955 23.6645 5.61438C21.4582 3.89827 20.2323 2.91761 18.0259 1.2015C17.2903 0.711177 15.8194 -0.0243073 15.084 0.711177C14.3484 1.44666 14.5936 2.18213 14.8387 3.40793C11.1614 3.65307 7.48395 5.12406 4.78719 7.82082C-1.83214 14.195 -1.58696 25.2272 5.52267 31.111C13.3677 37.7303 28.3227 35.2789 31.7547 25.2272C31.7547 23.5111 32 21.7949 32 20.3239Z"
            ></path>
        </svg>
    </div>
    <div v-if="itemsList[0]" class="option">
        <div class="contant">
            <button @click="flagInvert" class="close">
                <svg
                    width="20"
                    height="20"
                    viewBox="0 0 16 16"
                    xmlns="http://www.w3.org/2000/svg"
                    class=""
                >
                    <path
                        fill-rule="evenodd"
                        clip-rule="evenodd"
                        d="M15.5314 0.46863C14.9065 -0.15621 13.8934 -0.15621 13.2686 0.46863L7.99999 4.93727L2.73137 0.46863C2.10653 -0.156209 1.09347 -0.156209 0.468629 0.46863C-0.108145 1.04541 -0.152512 1.95297 0.335527 2.58064L0.468629 2.73137L5.73725 8.00001L0.468629 13.2686L0.335527 13.4194C-0.152512 14.0471 -0.108145 14.9546 0.468629 15.5314C1.09347 16.1562 2.10653 16.1562 2.73137 15.5314L7.99999 10.2627L13.2686 15.5314C13.8934 16.1562 14.9065 16.1562 15.5314 15.5314C16.1081 14.9546 16.1525 14.0471 15.6644 13.4194L15.5314 13.2686L11.0627 8.00001L15.5314 2.73137L15.6644 2.58064C16.1525 1.95297 16.1081 1.04541 15.5314 0.46863Z"
                    ></path>
                </svg>
            </button>
            <header class="header">
                <h4 class="main--title">{{ itemsList[0].itemName }}</h4>
                <p class="head--massa">вес {{ itemsList[0].itemMass }} гр</p>
            </header>
            <div class="wrapper">
                <div class="description">
                    <img class="description--image" :src="`./public/contant_images/${imageUrl}`" />
                    <div class="description--wrapper">
                        <h5 class="title">Информация</h5>
                        <p class="description--text">{{ itemsList[0].itemDescription }}</p>
                    </div>
                    <div class="description--control">
                        <button @click="dropdownFlag = !dropdownFlag" class="control--button">
                            <h5 class="title">Пищевая ценность:</h5>
                            <svg
                                :class="
                                    dropdownFlag ? 'description--icon' : 'description--icon_active'
                                "
                                viewBox="0 0 12 18"
                                xmlns="http://www.w3.org/2000/svg"
                            >
                                <path
                                    fill-rule="evenodd"
                                    clip-rule="evenodd"
                                    fill="currentColor"
                                    d="M1.217 9.82348C0.529075 9.15548 0.486089 8.09838 1.08802 7.38174L1.217 7.24317L8.12578 0.534397C8.85955 -0.178132 10.0492 -0.178132 10.783 0.534397C11.4709 1.2024 11.5139 2.2595 10.912 2.97612L10.783 3.11469L5.20284 8.53533L10.783 13.952C11.4709 14.6199 11.5139 15.677 10.912 16.3937L10.783 16.5322C10.0951 17.2002 9.00646 17.242 8.26846 16.6575L8.12576 16.5322L1.217 9.82348Z"
                                ></path>
                            </svg>
                        </button>
                        <div v-if="dropdownFlag" class="dropdown">
                            <div class="dropdown--buttons">
                                <button
                                    @click="changeMassCoefficient(0)"
                                    :class="
                                        !massCoefficientFlag
                                            ? 'dropdown--button_active ' + 'dropdown--button'
                                            : 'dropdown--button'
                                    "
                                >
                                    100 г
                                </button>
                                <button
                                    @click="changeMassCoefficient(1)"
                                    :class="
                                        massCoefficientFlag
                                            ? 'dropdown--button_active ' + 'dropdown--button'
                                            : 'dropdown--button'
                                    "
                                >
                                    {{ itemsList[0].itemMass }} гр
                                </button>
                            </div>
                            <ul v-if="dropdownFlag" class="dropdown--wrapper">
                                <li class="dropdown--item">
                                    <p class="item--name">
                                        {{ itemsList[0].itemNutritionalValue[0].nutritionalName }}
                                    </p>
                                    <p class="item--value">
                                        {{ calcNutrinicalValue(0) }}
                                    </p>
                                </li>
                                <li class="dropdown--item">
                                    <p class="item--name">
                                        {{ itemsList[0].itemNutritionalValue[1].nutritionalName }}
                                    </p>
                                    <p class="item--value">
                                        {{ calcNutrinicalValue(1) }}
                                    </p>
                                </li>
                                <li class="dropdown--item">
                                    <p class="item--name">
                                        {{ itemsList[0].itemNutritionalValue[2].nutritionalName }}
                                    </p>
                                    <p class="item--value">
                                        {{ calcNutrinicalValue(2) }}
                                    </p>
                                </li>
                                <li class="dropdown--item">
                                    <p class="item--name">
                                        {{ itemsList[0].itemNutritionalValue[3].nutritionalName }}
                                    </p>
                                    <p class="item--value">
                                        {{ calcNutrinicalValue(3) }}
                                    </p>
                                </li>
                                <li class="dropdown--item">
                                    <p class="item--name">
                                        {{ itemsList[0].itemNutritionalValue[4].nutritionalName }}
                                    </p>
                                    <p class="item--value">
                                        {{ calcNutrinicalValue(4) }}
                                    </p>
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
                <SupplementsList />
            </div>
            <footer class="footer">
                <p class="footer--text">Итого</p>
                <QuantityChange :bigSize="true" v-model="quantityProduct" :maxQuantity="99" />
                <button class="footer--button">789.89 Руб</button>
            </footer>
        </div>
    </div>
</template>

<style scoped>
.loading {
    display: flex;
    justify-content: center;
    align-items: center;
}

.loading--icon {
    height: 50px;
    width: 50px;
    animation-name: rotate-arrow;
    animation-duration: 0.8s;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
}

.close {
    position: absolute;
    display: flex;
    padding: 5px;
    top: 15px;
    right: 15px;
    fill: var(--color-border-light100);
    transition: fill 0.2s;
    z-index: 2;
    &:hover {
        fill: var(--color-text-brown300);
    }
}

.option {
    position: fixed;
    left: calc((100vw - var(--component-options-width)) / 2);
    top: calc((100vh - 550px) / 2);
    gap: 24px;
    width: var(--component-options-width);
    height: 550px;
    background-color: var(--color-bg-white100);
    border-radius: 24px;
    z-index: 1;
    overflow: hidden;
}

.contant {
    display: grid;
    grid-auto-flow: row;
    grid-template-rows: auto 1fr auto;
    height: 100%;
}

.header {
    background-color: var(--color-bg-white100);
    height: 58px;
    z-index: 1;
    display: flex;
    align-items: end;
    gap: 16px;
    padding: 24px 32px 10px;
    &::after {
        content: '';
        position: absolute;
        top: 58px;
        left: 0;
        width: 100%;
        height: 1px;
        background-color: var(--color-border-light100);
    }
}

.main--title {
    font-size: 1.625rem;
    line-height: 1.625rem;
}

.title {
    font-size: 1.25rem;
    font-weight: 500;
    line-height: 120%;
}

.head--massa {
    font-family: 'Rotonda';
    color: var(--color-text-browna500);
    font-size: 1rem;
    line-height: 1rem;
    font-weight: 500;
}

.wrapper {
    padding: 32px 24px;
    overflow: auto;
}

.description {
    display: grid;
    grid-template-columns: auto 1fr;
    grid-template-rows: auto auto;
    gap: 16px;
}

.description--wrapper {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
}

.description--food-value {
    display: grid;
    grid-auto-flow: column;
}

.description--icon {
    height: 16px;
    width: 16px;
    fill: var(--color-text-brown300);
    transform: rotate(90deg);
}

.description--icon_active {
    height: 16px;
    width: 16px;
    fill: var(--color-text-brown300);
    transform: rotate(270deg);
}

.description--image {
    grid-row: 1 / 3;
    width: 200px;
    object-fit: contain;
}

.description--text {
    font-family: 'Rotonda';
    margin-top: 16px;
    font-size: 0.875rem;
    line-height: 1rem;
    color: var(--color-text-brown300);
}

.control--button {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    color: var(--color-main-brown);
}

.dropdown {
    margin-top: 8px;
}

.dropdown--buttons {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 4px;
    border-radius: 30px;
    outline: 1px solid var(--color-text-light100);
}

.dropdown--button {
    font-size: 12px;
    padding: 4px 16px;
    color: var(--color-main-brown);
    border-radius: 30px;
    transition: 0.2;
}

.dropdown--button_active {
    background-color: var(--color-main-brown);
    color: var(--color-text-light200);
}

.dropdown--wrapper {
    display: flex;
    gap: 8px;
    margin-top: 12px;
}

.dropdown--item {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 5px;
    padding: 4px 8px;
}

.item--name {
    font-family: 'Rotonda';
    font-size: 1rem;
    font-weight: 500;
    color: var(--color-text-browna600);
}

.item--value {
}

.footer {
    position: relative;
    background-color: var(--color-bg-white100);
    height: 77px;
    z-index: 1;
    display: flex;
    align-items: end;
    gap: 16px;
    padding: 24px 32px 10px;
    &::after {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 1px;
        background-color: var(--color-border-light100);
    }
}

@keyframes rotate-arrow {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}
</style>
