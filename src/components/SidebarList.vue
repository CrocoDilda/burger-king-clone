<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

import SidebarItem from './SidebarItem.vue'

defineProps({
    tabState: Number
})

// получаю данные с бэка
const categoriesList = ref([])
onMounted(async () => {
    try {
        const { data } = await axios.get('https://14c3bbbcd96e00ef.mokky.dev/categories-list')
        categoriesList.value = data
    } catch (error) {
        console.log(error)
    }
})
</script>

<template>
    <aside>
        <ul class="aside">
            <SidebarItem
                v-for="item in categoriesList"
                :key="item.categoryId"
                :imageUrl="item.categoryImageUrl"
                :title="item.categoryTitle"
                :tabState="tabState"
            />
            <!-- <SidebarItem title="Все рестораны" imageUrl="icons/food.png" /> -->
        </ul>
    </aside>
</template>

<style scoped>
.aside {
    position: sticky;
    top: 112px;
    background-color: var(--color-bg-gray300);
    display: flex;
    flex-direction: column;
    align-items: start;
    margin-top: 32px;
    max-height: 765px;
    border-radius: 20px;
    overflow-y: auto;
    scroll-behavior: smooth;
    &::-webkit-scrollbar {
        display: none;
    }
}
</style>
