<script setup>
import { inject } from 'vue'
import ComboVarieties from './ComboVarieties.vue'
defineProps({
    imageUrl: String,
    itemId: Number
})

const changeIndexIvent = inject('changeIndexIvent')
</script>

<template>
    <div class="options">
        <button @click="changeIndexIvent" class="close">
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
        <div class="title-block">
            <img class="title--image" :src="`../../public/contant_images/${imageUrl}`" />
            <h3 class="title">Составить комбо?</h3>
        </div>
        <ul class="combo">
            <ComboVarieties
                :imageUrl="imageUrl"
                :price="500.99"
                title="Мне только Ангус По-Итальянски"
            />
            <ComboVarieties
                :imageUrl="imageUrl"
                :price="500.99"
                benefit="Выгода до 25%"
                title="Мини комбо"
            />
            <ComboVarieties
                :imageUrl="imageUrl"
                :price="500.99"
                :isBest="true"
                benefit="Выгода до 25%"
                title="Мидл комбо"
            />
            <ComboVarieties
                :imageUrl="imageUrl"
                :price="500.99"
                benefit="Выгода до 25%"
                title="Биг комбо"
            />
        </ul>
    </div>
</template>

<style scoped>
.close {
    position: absolute;
    display: flex;
    padding: 5px;
    top: 24px;
    right: 24px;
    fill: var(--color-border-light100);
    transition: fill 0.2s;
    &:hover {
        fill: var(--color-text-brown300);
    }
}

.options {
    position: fixed;
    left: calc((100vw - var(--component-options-width)) / 2);
    top: 1.5vh;
    display: flex;
    flex-direction: column;
    gap: 24px;
    padding: 48px 56px 56px;
    width: var(--component-options-width);
    height: 97vh;
    background-color: var(--color-bg-white100);
    border-radius: 24px;
    z-index: 1;
}

.title-block {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.combo {
    display: grid;
    gap: 12px;
    width: 100%;
}
</style>
