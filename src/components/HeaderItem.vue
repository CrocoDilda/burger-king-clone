<script setup>
import { ref } from 'vue'

import Dropdown from './Dropdown.vue'

defineProps({
    recervingOrderTo: {
        type: String,
        default: 'В РЕСТОРАНЕ'
    },
    choisedPlaced: {
        type: String,
        default: 'Для заказа выбери ресторан'
    },
    basketIsDisabled: {
        type: Boolean,
        default: true
    },
    baskerCount: {
        type: Number,
        default: 12333
    },
    tabState: Number
})

const emit = defineEmits(['tabInvert'])

const headerInputValue = ref('')
const popUpState = ref(false)

function invertPopUpState() {
    popUpState.value = !popUpState.value
    emit('tabInvert')
}
</script>

<template>
    <header class="header">
        <Dropdown v-if="popUpState" @popUpFunction="invertPopUpState" />
        <div class="header--wrapper container">
            <div class="options">
                <button
                    :tabindex="tabState"
                    @click="
                        () => {
                            invertPopUpState()
                        }
                    "
                    class="button--dropdown"
                >
                    <div class="dropdown--item"></div>
                    <div class="dropdown--item"></div>
                    <div class="dropdown--item"></div>
                </button>
                <button :tabindex="tabState" class="button--receiving">
                    <span
                        >{{ recervingOrderTo }}

                        <svg
                            class="receiving--icon"
                            width="14"
                            height="14"
                            viewBox="0 0 14 14"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <path
                                fill-rule="evenodd"
                                clip-rule="evenodd"
                                d="M12.8349 2.29155L11.7073 1.16377C11.192 0.648521 10.3537 0.648546 9.83846 1.16377L9.39707 1.60519L12.3936 4.60192L12.8349 4.1605C13.3514 3.64403 13.3515 2.80807 12.8349 2.29155ZM1.31284 9.93439L0.783931 12.7908C0.76208 12.9089 0.799705 13.0301 0.884604 13.115C0.969601 13.2 1.09089 13.2376 1.20879 13.2157L4.06499 12.6867L1.31284 9.93439ZM1.70626 9.29658L8.88149 2.12081L11.878 5.11753L4.70275 12.2933L1.70626 9.29658Z"
                            />
                        </svg>
                    </span>
                    <p>{{ choisedPlaced }}</p>
                </button>
                <label class="label">
                    <div class="label--button label--search">
                        <img src="../../public/icons/search-light.f1e6950.svg" alt="search" />
                    </div>
                    <input
                        :tabindex="tabState"
                        @input="$emit(input.value)"
                        v-model="headerInputValue"
                        type="text"
                        class="input"
                        placeholder="Введите название блюда"
                    />
                    <button
                        :tabindex="tabState"
                        @click="headerInputValue = ''"
                        class="label--button label--close"
                    >
                        <svg
                            width="16"
                            height="16"
                            viewBox="0 0 16 16"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <path
                                fill-rule="evenodd"
                                clip-rule="evenodd"
                                d="M15.5314 0.46863C14.9065 -0.15621 13.8934 -0.15621 13.2686 0.46863L7.99999 4.93727L2.73137 0.46863C2.10653 -0.156209 1.09347 -0.156209 0.468629 0.46863C-0.108145 1.04541 -0.152512 1.95297 0.335527 2.58064L0.468629 2.73137L5.73725 8.00001L0.468629 13.2686L0.335527 13.4194C-0.152512 14.0471 -0.108145 14.9546 0.468629 15.5314C1.09347 16.1562 2.10653 16.1562 2.73137 15.5314L7.99999 10.2627L13.2686 15.5314C13.8934 16.1562 14.9065 16.1562 15.5314 15.5314C16.1081 14.9546 16.1525 14.0471 15.6644 13.4194L15.5314 13.2686L11.0627 8.00001L15.5314 2.73137L15.6644 2.58064C16.1525 1.95297 16.1081 1.04541 15.5314 0.46863Z"
                            ></path>
                        </svg>
                    </button>
                </label>
            </div>
            <button :tabindex="tabState" class="logo">
                <img src="../../public/icons/logo.de57e07.svg" alt="BK" />
            </button>
            <nav class="pagination">
                <ul class="pagination--list">
                    <li><button :tabindex="tabState" class="pagination--button">РАБОТА</button></li>
                    <li><button :tabindex="tabState" class="pagination--button">КУПОНЫ</button></li>
                    <li>
                        <button :tabindex="tabState" class="pagination--button">KING CLUB</button>
                    </li>
                    <li>
                        <button :tabindex="tabState" class="pagination--button">
                            <svg
                                class="pagination--icon"
                                width="24"
                                height="24"
                                viewBox="0 0 24 24"
                                fill="none"
                                xmlns="http://www.w3.org/2000/svg"
                            >
                                <path
                                    fill-rule="evenodd"
                                    clip-rule="evenodd"
                                    d="M17.4545 5.45455C17.4545 8.467 15.0124 10.9091 12 10.9091C8.98754 10.9091 7.18545 8.467 6.78545 5.45455C6.38545 2.4421 8.98754 0 12 0C15.0124 0 17.4545 2.44209 17.4545 5.45455ZM0.4 18.6542L0 22.6969L24 23.4969V18.6542C24 15.4645 21.0153 12.8787 17.3333 12.8787H6.66667C2.98477 12.8787 0.4 15.4645 0.4 18.6542Z"
                                    fill="currentColor"
                                ></path>
                            </svg>
                            ВОЙТИ
                        </button>
                    </li>
                    <li>
                        <button
                            :tabindex="tabState"
                            :disabled="basketIsDisabled"
                            class="pagination--basket"
                        >
                            <svg
                                width="16"
                                height="18"
                                viewBox="0 0 16 18"
                                xmlns="http://www.w3.org/2000/svg"
                                class="bk-cart-icon"
                            >
                                <path
                                    fill-rule="evenodd"
                                    clip-rule="evenodd"
                                    fill="currentColor"
                                    d="M7.72094 0.327103C5.97472 0.327103 4.92699 1.37483 4.34492 2.6554H6.20755C6.55679 2.30616 7.02245 1.95691 7.72094 1.95691C8.53583 1.84049 9.11793 1.95691 9.35075 2.6554H11.097C11.0745 2.58814 11.0521 2.51656 11.0289 2.44233C10.9314 2.13111 10.8193 1.77323 10.6313 1.49125C10.0492 0.443518 8.76867 0.327103 7.72094 0.327103ZM14.7058 4.16878C14.7058 4.16878 15.1714 12.3178 15.4043 15.3446C15.4182 15.5523 15.4369 15.7435 15.4542 15.9192C15.582 17.2211 15.6264 17.6729 12.9596 17.6729H6.09114C4.46134 17.6729 2.83151 17.6729 1.55096 17.5564C0.48631 17.5564 0.492688 16.9722 0.501555 16.1601C0.502384 16.0842 0.503234 16.0063 0.503234 15.9267L0.968886 4.16878H3.99568H5.39264H14.7058Z"
                                ></path>
                            </svg>
                            <p>{{ baskerCount }}</p>
                        </button>
                    </li>
                </ul>
            </nav>
        </div>
    </header>
</template>

<style scroped>
.header {
    position: sticky;
    top: 0;
    left: 0;
    width: 100vw;
    z-index: 10;
    border-bottom: 2px solid var(--color-border-light100);
}

.header--wrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: relative;
    background-color: var(--color-bg-white100);
    width: 100%;
    height: 83px;
}

.options {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 20px;
}

.button--dropdown {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    height: 30px;
    width: 32px;
    padding: 2px 0;
    background-color: transparent;
    transition:
        padding 0.2s,
        transform 0.2s;
    &:hover {
        padding: 0;
        transform: scale(1.1);
    }
}

.dropdown--item {
    height: 3px;
    width: 100%;
    background-color: var(--color-main-brown);
    border-radius: 1px;
    transition: width 0.2s;
}

.button--receiving {
    display: flex;
    flex-direction: column;
    background-color: transparent;
    fill: var(--color-main-brown);
    transition:
        color 0.2s,
        fill 0.2s,
        transform 0.2s;
    &:hover {
        color: var(--color-text-brown400);
        fill: var(--color-text-brown400);
        transform: scale(1.05);
    }
}

.button--receiving span {
    display: flex;
    align-items: start;
    justify-content: center;
    gap: 10px;
}

.button--receiving p {
    font-family: 'Rotonda';
    font-weight: 500;
}

.label {
    position: relative;
}

.label--button {
    position: absolute;
    background-color: transparent;
}

.label--search {
    left: 5%;
    top: 7px;
}

.label--close {
    display: flex;
    align-items: center;
    right: 5%;
    top: 9px;
    fill: var(--color-border-light100);
    transition: fill 0.2s;
    &:hover {
        fill: var(--color-text-brown300);
    }
}

.input {
    border-radius: 25px;
    padding: 8px 40px;
    width: 250px;
    background-color: var(--color-bg-white);
    border: 1px solid var(--color-border-light100);
    font-family: 'Rotonda';
    font-weight: 500;
    color: var(--color-main-brown);
    transition: outline 0.1s;
    &::placeholder {
        color: var(--color-text-light100);
    }
    &:hover {
        outline: 3px solid var(--color-main-brown);
    }
}

.logo {
    position: absolute;
    top: calc(50% - 27px);
    left: calc(50% - 27px);
    background-color: transparent;
    transition: transform 0.2s;
    &:hover {
        transform: scale(1.1);
    }
}

.logo img {
    height: 54px;
    width: 54px;
}

.pagination--list {
    display: flex;
    align-items: center;
    gap: 15px;
}

.pagination--button {
    display: flex;
    align-items: center;
    font-size: 0.875rem;
    color: var(--color-main-brown);
    transition:
        transform 0.2s,
        color 0.2s;
    &:hover {
        color: var(--color-text-brown400);
        transform: scale(1.05);
    }
}

.pagination--button img {
    height: 21px;
    width: 21px;
}

.pagination--icon {
    margin-right: 5px;
    height: 21px;
    width: 21px;
}

.pagination--basket {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1rem;
    background-color: var(--color-main-brown);
    gap: 10px;
    padding: 8px 15px;
    min-width: 76px;
    border-radius: 24px;
    color: var(--color-text-light200);
    transition:
        transform 0.2s,
        background-color 0.2s,
        disabled 0.2s;
    &:disabled {
        background-color: var(--color-text-light100);
        cursor: auto;
    }
    &:hover {
        background-color: var(--color-text-brown400);
        transform: scale(1.05);
    }
    &:disabled:hover {
        background-color: var(--color-text-light100);
        transform: scale(1);
    }
}

.pagination--basket p {
    margin-top: 3px;
}
</style>
