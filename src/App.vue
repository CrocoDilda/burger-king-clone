<script setup>
import { onMounted, provide, ref } from 'vue'
import axios from 'axios'

import HomeView from './pages/HomeView.vue'
import HeaderItem from './components/HeaderItem.vue'
import FooterItem from './components/FooterItem.vue'

// получаю данные с бэка
const categoriesList = ref([])
onMounted(() => {
    try {
        const { data } = axios.get('https://14c3bbbcd96e00ef.mokky.dev/categories-list')
        categoriesList.value = data
    } catch (error) {
        console.log(error)
    }
})

// блокировщик табуляции
const tabState = ref(0)
const tabInvert = () => {
    if (tabState.value === -1) {
        tabState.value = 0
        document.body.style.overflowY = 'auto'
    } else {
        tabState.value = -1
        document.body.style.overflowY = 'hidden'
    }
}

provide('tabInvert', tabInvert)
</script>

<template>
    <h1 class="warning">
        Внимание! Данный проект сделан искючительно в учебных целях и несёт за собой следующие
        задачи: практиковать фреймворк Vue.js, улучшить UX и адаптив оригинального сайта
        burger-king, т.к. у них это сделанно так себе. <br />
        4.07.24 в оригинальном сайте бк произошло обновление, немного поменялся дизайн, но не стоит
        переживать, косяков там всё равно дофига. Мне лень переделывать уже готовые элементы, да и
        цели сделать идеальный клон нет. Поэтому я слеплю химеру.
    </h1>
    <HeaderItem :tabState="tabState" :basketIsDisabled="true" @tabInvert="tabInvert" />
    <HomeView :tabState="tabState" />
    <FooterItem />
</template>

<style scoped>
.warning {
    text-align: center;
    background-color: #fa4747;
    padding: 20px;
    font-size: 1rem;
}
</style>
