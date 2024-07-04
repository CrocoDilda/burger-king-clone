<script setup>
defineProps({
    bigSize: Boolean,
    maxQuantity: Number
})

const model = defineModel()

function increment() {
    model.value++
}

function decrement() {
    model.value--
}
</script>

<template>
    <div v-if="bigSize === true" class="inner inner_big">
        <button
            :disabled="model < 2 ? true : false"
            @click="decrement"
            class="button minus minus_big"
        >
            -
        </button>
        <p class="quantity quantity_big">{{ model }}</p>
        <button
            :disabled="model >= maxQuantity ? true : false"
            @click="increment"
            class="button plus plus_big"
        >
            +
        </button>
    </div>
    <div v-else class="inner inner_small">
        <button
            :disabled="model < 1 ? true : false"
            @click="decrement"
            class="button minus minus_small"
        >
            -
        </button>
        <p class="quantity quantity_small">{{ model }}</p>
        <button
            :disabled="model >= maxQuantity ? true : false"
            @click="increment"
            class="button plus plus_small"
        >
            +
        </button>
    </div>
</template>

<style scoped>
.inner {
    display: grid;
    grid-auto-flow: column;
    grid-template-columns: repeat(3, 1fr);
    justify-content: center;
    align-content: center;
    border-radius: 55px;
}

.inner_small {
    padding: 2px;
    width: 100%;
    border: 1px solid #d7c7b4;
}

.inner_big {
    padding: 5px;
    width: 122px;
    border: 2px solid #d7c7b4;
}

.button {
    position: relative;
    background-color: var(--color-main-brown);
    border-radius: 40px;
    transition: 0.2s;
    &:after {
        content: '';
        position: absolute;
        top: 50%;
        left: 50%;
        height: 8%;
        width: 60%;
        border-radius: 2px;
        background-color: var(--color-bg-white);
        transform: translate(-50%, -50%);
    }
    &:hover {
        background-color: var(--color-text-brown300);
    }
    &:disabled {
        opacity: 0.2;
        cursor: default;
        &:hover {
            background-color: var(--color-main-brown);
            opacity: 0.2;
        }
    }
}

.plus {
    justify-self: end;
    &:before {
        content: '';
        position: absolute;
        top: 50%;
        left: 50%;
        width: 8%;
        height: 60%;
        border-radius: 2px;
        background-color: var(--color-bg-white);
        transform: translate(-50%, -50%);
    }
}

.plus_small {
    height: 24px;
    width: 24px;
}

.plus_big {
    height: 36px;
    width: 36px;
}

.minus_small {
    height: 24px;
    width: 24px;
}

.quantity {
    display: flex;
    align-items: center;
    justify-content: center;
}

.quantity_big {
    font-size: 1.125rem;
    padding-top: 4px;
}
</style>
