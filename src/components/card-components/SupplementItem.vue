<script setup>
import { ref } from 'vue'
import QuantityChange from '../controls/QuantityChange.vue'
defineProps({
    item: Object
})

const quantitySupplement = ref(0)
function incrementQuantitySupplement() {
    if (quantitySupplement.value === 0) {
        quantitySupplement.value++
    }
}
</script>

<template>
    <li class="wrapper">
        <img class="image" :src="`../../../public/supplements/${item.image}`" alt="" />
        <p class="name">{{ item.name }}</p>
        <p class="price">{{ item.price }} ₽</p>
        <div class="quantity">
            <QuantityChange
                v-show="quantitySupplement > 0"
                v-model="quantitySupplement"
                :maxQuantity="item.maxValue"
            />
            <button
                @click="incrementQuantitySupplement"
                v-show="quantitySupplement <= 0"
                class="plus"
            ></button>
        </div>
    </li>
</template>

<style scoped>
.item {
}

.wrapper {
    display: grid;
    grid-auto-flow: row;
    grid-template-rows: 80px 1fr;
    justify-content: center;
    gap: 5px;
    padding: 4px 8px 8px;
    width: 128px;
    background-color: var(--color-bg-gray300);
    border-radius: 16px;
}

.wrapper--active {
    background-color: white;
}

.image {
    width: 80px;
    justify-self: center;
    align-self: center;
}

.price {
    font-size: 0.875rem;
    color: var(--color-border-brown100);
    padding: 1px 2px;
    font-size: 0.875rem;
    text-align: center;
}

.name {
    font: 500 12px / 1rem 'Rotonda';
    color: var(--color-text-brown300);
    text-align: start;
    text-align: center;
}

.quantity {
    display: flex;
    justify-content: center;
    height: 32px;
}

.plus {
    position: relative;
    border: 2px solid var(--color-border-light100);
    border-radius: 50px;
    height: 32px;
    width: 32px;
    text-align: center;
    transition: 0.2s;
    &::after {
        content: '';
        position: absolute;
        top: 50%;
        left: 50%;
        height: 4px;
        width: 17px;
        border-radius: 2px;
        background-color: var(--color-text-brown300);
        transform: translate(-50%, -50%);
    }
    &::before {
        content: '';
        position: absolute;
        top: 50%;
        left: 50%;
        width: 4px;
        height: 17px;
        border-radius: 2px;
        background-color: var(--color-text-brown300);
        transform: translate(-50%, -50%);
    }
    &:hover {
        transform: scale(1.1);
        box-shadow: 0 0 3px var(--color-main-brown);
    }
}

.quantity-change {
    display: flex;
    justify-content: center;
    margin-top: 18px;
    height: 32px;
}
</style>
