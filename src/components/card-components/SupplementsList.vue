<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

import SupplementItem from './SupplementItem.vue'

// Данные о продукте
const itemsList = ref([])
onMounted(async () => {
    try {
        const { data } = await axios.get(`https://14c3bbbcd96e00ef.mokky.dev/supplements`)
        itemsList.value = data
    } catch (error) {
        console.log(error)
    }
})
</script>

<template>
    <ul class="list">
        <SupplementItem v-for="item in itemsList" :key="item.itemId" :item="item" />
    </ul>
</template>

<style scoped>
.list {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
}

.image {
    width: 80px;
}
</style>
