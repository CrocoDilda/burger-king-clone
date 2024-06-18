<script setup>
import axios from 'axios'
import { onMounted, ref } from 'vue'

import SliderItem from './SliderItem.vue'

defineProps({
    tabState: Number
})

const itemsList = ref([])

onMounted(async () => {
    try {
        const { data } = await axios.get('https://14c3bbbcd96e00ef.mokky.dev/slider')
        itemsList.value = data
    } catch (error) {
        console.log(error)
    }
})

// console.log(element.clientX)
// element.target.scrollLeft += 50
</script>

<template>
    <section class="section">
        <SliderItem
            v-for="item in itemsList"
            :key="item.itemId"
            :image-url="item.itemImageUrl"
            :title="item.itemTitle"
            :tabState="tabState"
        />
    </section>
</template>

<style scoped>
.section {
    display: flex;
    gap: 48px;
    position: relative;
    padding: 32px 80px;
    background-color: var(--color-main-brown);
    height: 300px;
    min-width: 100vw;
    overflow-x: auto;
    &::-webkit-scrollbar {
        display: none;
    }
}
</style>
