<script setup>
defineProps({
    imageUrl: String,
    title: String,
    tabState: Number
})
</script>

<template>
    <li>
        <a :tabindex="tabState" class="link" href="#">
            <div class="wrapper">
                <img class="image" :src="`../../public/slider_images/${imageUrl}`" />
            </div>
            <h3 class="title">{{ title }}</h3>
        </a>
    </li>
</template>

<style scoped>
li {
    list-style-type: none;
}

.link:focus-visible .wrapper {
    outline: 5px solid var(--color-border-light200);
}

.link .wrapper {
    outline: 1px solid var(--color-border-brown100);
    transition: 0.2s;
}

.link:hover .wrapper {
    outline: 5px solid var(--color-border-light200);
    transform: scale(1.05);
}

.link .title {
    font-family: 'Rotonda';
    font-size: 1.125rem;
    font-weight: 500;
    text-align: center;
    color: var(--color-text-light300);
    margin-top: 10px;
    text-transform: uppercase;
}

.link:hover .title {
    color: var(--color-border-light200);
    font-weight: 700;
}

.wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 220px;
    width: 220px;
    border-radius: 50%;
}

.image {
    height: 188px;
    width: 188px;
    border-radius: 50%;
}
</style>
