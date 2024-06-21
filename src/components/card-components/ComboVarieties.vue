<script setup>
defineProps({
    imageUrl: String,
    price: Number,
    isBest: Boolean,
    benefit: String,
    title: String
})
</script>

<template>
    <li class="combo--li" v-if="isBest">
        <button class="combo--item best--item">
            <img class="combo--image" :src="`../../public/contant_images/${imageUrl}`" alt="" />
            <div class="combo--wrapper">
                <h4 class="combo--title">{{ title }}</h4>
                <p class="combo--text">
                    <span class="best--price combo--price">{{ price }}</span> {{ benefit }}
                </p>
            </div>
            <div class="arrow">
                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="18" viewBox="0 0 12 18">
                    <path
                        fill-rule="evenodd"
                        clip-rule="evenodd"
                        fill="#845F50"
                        d="M1.217 9.82348C0.529075 9.15548 0.486089 8.09838 1.08802 7.38174L1.217 7.24317L8.12578 0.534397C8.85955 -0.178132 10.0492 -0.178132 10.783 0.534397C11.4709 1.2024 11.5139 2.2595 10.912 2.97612L10.783 3.11469L5.20284 8.53533L10.783 13.952C11.4709 14.6199 11.5139 15.677 10.912 16.3937L10.783 16.5322C10.0951 17.2002 9.00646 17.242 8.26846 16.6575L8.12576 16.5322L1.217 9.82348Z"
                    />
                </svg>
            </div>
        </button>
    </li>
    <li class="combo--li" v-else>
        <button class="combo--item">
            <img class="combo--image" :src="`../../public/contant_images/${imageUrl}`" alt="" />
            <div class="combo--wrapper">
                <h4 class="combo--title">{{ title }}</h4>
                <p class="combo--text">
                    <span class="combo--price">{{ price }}</span> {{ benefit }}
                </p>
            </div>
            <div class="arrow">
                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="18" viewBox="0 0 12 18">
                    <path
                        fill-rule="evenodd"
                        clip-rule="evenodd"
                        fill="#845F50"
                        d="M1.217 9.82348C0.529075 9.15548 0.486089 8.09838 1.08802 7.38174L1.217 7.24317L8.12578 0.534397C8.85955 -0.178132 10.0492 -0.178132 10.783 0.534397C11.4709 1.2024 11.5139 2.2595 10.912 2.97612L10.783 3.11469L5.20284 8.53533L10.783 13.952C11.4709 14.6199 11.5139 15.677 10.912 16.3937L10.783 16.5322C10.0951 17.2002 9.00646 17.242 8.26846 16.6575L8.12576 16.5322L1.217 9.82348Z"
                    />
                </svg>
            </div>
        </button>
    </li>
</template>

<style scoped>
.combo--li {
    width: 100%;
}

.combo--item {
    display: flex;
    gap: 20px;
    position: relative;
    width: 100%;
    background-color: var(--color-bg-white200);
    padding: 15px 20px 15px 30px;
    border-radius: 10px;
    min-height: 10px;
    transition: 0.1s;
    &:hover {
        transform: scale(1.05);
        box-shadow: 0px 0px 10px var(--color-main-brown);
    }
}

.combo--image {
    width: 80px;
}

.combo--wrapper {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: start;
    width: 100%;
    height: 80px;
}

.combo--title {
    font-size: 1.25rem;
    color: var(--color-main-brown);
}

.combo--text {
    display: flex;
    gap: 15px;
    align-items: center;
    color: var(--color-text-green100);
    font-size: 1rem;
}

.combo--price {
    border: 1px solid var(--color-text-brown300);
    border-radius: 60px;
    padding: 7px;
    text-align: center;
    width: 90px;
    font-family: 'Rotonda';
    font-weight: 500;
    color: var(--color-main-brown);
}

.best--price {
    border: 1px solid var(--color-text-green100);
    color: #fff;
    background-color: var(--color-text-green100);
}

.arrow {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    right: 10px;
    top: calc(50% - 16px);
    transform: rotate(180deg);
    height: 32px;
    width: 32px;
    border-radius: 50%;
    background-color: var(--color-bg-white100);
}

.best--item {
    background-color: #fff;
}
</style>
