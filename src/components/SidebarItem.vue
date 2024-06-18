<script setup>
defineProps({
    imageUrl: String,
    title: String,
    tabState: Number
})
</script>

<template>
    <li>
        <button :tabindex="tabState" class="wrapper">
            <img class="image" :src="`/public/contant_images/${imageUrl}`" />
            <h3 class="title">{{ title }}</h3>
        </button>
    </li>
</template>

<style scoped>
li {
    width: 100%;
}

.wrapper {
    display: flex;
    align-items: center;
    position: relative;
    gap: 12px;
    padding: 8px 12px;
    width: 100%;
    transition: 0.2s;
    &:hover {
        background-color: var(--color-border-light200);
        transform: scale(1.05);
    }
}

.acrive-efect {
    background-color: var(--color-bg-white);
}

.image {
    height: 48px;
    width: 48px;
}

.title {
    font-size: 1rem;
    white-space: nowrap;
}
</style>
