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
    console.log('сейчас tabState = ' + tabState.value)
}

provide('tabInvert', tabInvert)
</script>

<template>
    <HeaderItem :tabState="tabState" :basketIsDisabled="true" @tabInvert="tabInvert" />
    <HomeView :tabState="tabState" />
    <FooterItem />
</template>

<style scoped></style>
