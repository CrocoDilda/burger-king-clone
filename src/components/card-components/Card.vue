<script setup>
import { ref, inject, provide } from 'vue'
import CardAdditionally from './CardAdditionally.vue'

defineProps({
    itemName: String,
    itemPrice: Number,
    itemImageUrl: String,
    itemType: String,
    tabState: Number,
    itemId: Number
})

const flag = ref(false)
const tabInvert = inject('tabInvert')

function flagInvert() {
    flag.value = !flag.value
    tabInvert()
}
provide('flagInvert', flagInvert)
</script>

<template>
    <li>
        <button @click="flagInvert()" :tabindex="tabState" class="card">
            <img class="image" :src="`./public/contant_images/${itemImageUrl}`" :alt="itemType" />
            <h3 class="title">{{ itemName }}</h3>
            <div class="description">
                <p class="price">{{ itemPrice }} ₽</p>
                <p class="pseudo-button">Заказать</p>
            </div>
        </button>
    </li>
    <CardAdditionally v-if="flag" :imageUrl="itemImageUrl" :itemId="itemId" />
</template>

<style scoped>
.card {
    display: grid;
    align-items: start;
    gap: 15px;
    justify-content: space-evenly;
    padding: 24px;
    width: 100%;
    height: 100%;
    max-height: 400px;
    border-radius: 20px;
    background-color: var(--color-bg-gray300);
    transition: 0.2s;
    &:hover {
        background-color: var(--color-border-light200);
        box-shadow: 0px 0px 10px var(--color-main-brown);
        transform: scale(1.01);
    }
}

.image {
    width: 100%;
    max-height: 250px;
    object-fit: contain;
}

.title {
    font-size: 1.125rem;
    text-align: start;
    color: var(--color-main-brown);
}

.description {
    display: flex;
    gap: 5px;
    justify-content: space-between;
    align-items: center;
}

.price {
    font-size: 1.5rem;
    color: var(--color-main-brown);
    white-space: nowrap;
}

.pseudo-button {
    background-color: #ff6e20;
    border-radius: 20px;
    color: #f5ebdc;
    font-size: 16px;
    line-height: 140%;
    padding: 9px 24px;
}
</style>
