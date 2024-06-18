<!-- parent -->

<script setup>
import { ref } from 'vue'
import AppExperement from './pages/AppExperement.vue'

const tabState = ref(0)

const tabInvert = () => {
    tabState.value === -1 ? (tabState.value = 0) : (tabState.value = -1)
}
</script>

<template>
    <AppExperement @tabInvert="tabInvert" :tabValue="tabState.value" />
    <p>Сейчас переменная равна {{ tabState }}</p>
</template>

<!-- child -->
<script setup>
defineProps({
    tabValue: Number
})

const emit = defineEmits(['tabInvert'])
</script>

<template>
    <button @click="() => emit('tabInvert')">
        При нажатии я должен получить изменение значения в App
    </button>
</template>

<style scoped>
button {
    background-color: #4d4d4d;
    color: white;
    padding: 20px;
    border-radius: 10px;
    margin: 40px;
    &:active {
        background-color: #949494;
    }
}
</style>
