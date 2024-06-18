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

provide('tab', 1)
// provide('changeTab', changeTabIndexValue)
</script>

<template>
    <HeaderItem v-model="tabIndexValue" :basketIsDisabled="true" />
    <HomeView />
    <FooterItem />
</template>

<style scoped></style>
