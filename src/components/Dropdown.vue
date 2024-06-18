<script setup>
const emit = defineEmits(['popUpFunction'])
</script>

<template>
    <div class="wrapper">
        <div @click="() => emit('popUpFunction')" class="bg-filter"></div>
        <div class="dropdown container">
            <button @click="() => emit('popUpFunction')" class="closed">
                <svg
                    width="16"
                    height="16"
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
            <nav class="nav">
                <ul class="nav--list">
                    <li>
                        <a class="nav--item" href="#">Меню</a>
                    </li>
                    <li>
                        <a class="nav--item" href="#">Купоны</a>
                    </li>
                    <li>
                        <a class="nav--item" href="#">King Club</a>
                    </li>
                    <li>
                        <a class="nav--item" href="#">Работа</a>
                    </li>
                    <li>
                        <a class="nav--item" href="#">FAQ</a>
                    </li>
                    <li>
                        <a class="nav--item" href="#">Контакты</a>
                    </li>
                </ul>
            </nav>
            <ul class="we">
                <li><a class="we--item" href="#">Новинки и акции</a></li>
                <li><a class="we--item" href="#">Развитие</a></li>
                <li><a class="we--item" href="#">О компании</a></li>
                <li><a class="we--item" href="#">Тендеры</a></li>
                <li><a class="we--item" href="#">Рестораны</a></li>
                <li><a class="we--item" href="#">Для детей</a></li>
                <li><a class="we--item" href="#">Партнёры</a></li>
                <li><a class="we--item" href="#">Мобильное приложение</a></li>
            </ul>
        </div>
    </div>
</template>

<style scoped>
.wrapper {
    transition: 0.2s;
}

.dropdown {
    display: flex;
    position: absolute;
    top: 83px;
    height: calc(100vh - 83px);
    background-color: var(--color-bg-white100);
    width: 42vw;
    padding-top: 48px;
    padding-bottom: 40px;
}

.closed {
    position: absolute;
    padding: 5px;
    top: 33px;
    right: 30px;
    display: flex;
    fill: var(--color-border-light100);
    transition: fill 0.2s;
    &:hover {
        fill: var(--color-text-brown300);
    }
}

.nav--list {
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin-right: 74px;
}

.nav--item {
    font-size: 1.625rem;
    color: var(--color-main-brown);
    white-space: nowrap;
    transition: color 0.2s;
    &:hover {
        color: var(--color-text-brown400);
    }
}

.we {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.we--item {
    font-size: 1rem;
    color: var(--color-main-brown);
    font-family: 'Rotonda';
    white-space: nowrap;
    transition: color 0.2s;
    &:hover {
        color: var(--color-text-brown400);
    }
}
</style>
