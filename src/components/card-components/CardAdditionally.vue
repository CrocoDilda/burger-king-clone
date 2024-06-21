<script setup>
import { ref, inject, provide } from 'vue'
import CardCombo from './CardCombo.vue'
import CardOptions from './CardOptions.vue'
defineProps({
    imageUrl: String,
    itemId: Number
})

const eventakStageIndex = ref(true)
const flagInvert = inject('flagInvert')

function changeIndexIvent() {
    if (eventakStageIndex.value === false) {
        flagInvert()
    }
    eventakStageIndex.value = !eventakStageIndex.value
}

provide('changeIndexIvent', changeIndexIvent)
</script>

<template>
    <div class="wrapper">
        <div @click="changeIndexIvent()" class="bg-filter"></div>
        <CardCombo v-if="eventakStageIndex" :itemId="itemId" :imageUrl="imageUrl" />
        <CardOptions v-else :itemId="itemId" :imageUrl="imageUrl" />
    </div>
</template>

<style scoped>
.wrapper {
    position: fixed;
    z-index: 19;
}
</style>
