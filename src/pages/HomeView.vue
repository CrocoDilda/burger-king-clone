<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

import CardsList from '../components/CardsList.vue'
import SidebarList from '../components/SidebarList.vue'
import SliderList from '../components/SliderList.vue'

defineProps({
    tabState: Number
})

const itemsList = ref([])
onMounted(async () => {
    try {
        const { data } = await axios.get('https://14c3bbbcd96e00ef.mokky.dev/items-v2')
        itemsList.value = data
    } catch (error) {
        console.log(error)
    }
})
</script>

<template>
    <main>
        <SliderList :tabState="tabState" />
        <section class="hero container">
            <SidebarList :tabState="tabState" />
            <div class="wrapper">
                <CardsList :tabState="tabState" :itemsList="itemsList" />
                <CardsList :tabState="tabState" :itemsList="itemsList" />
                <CardsList :tabState="tabState" :itemsList="itemsList" />
                <CardsList :tabState="tabState" :itemsList="itemsList" />
            </div>
        </section>
    </main>
</template>

<style scoped>
.main {
    &:focus-visible {
        outline: 0px solid var(--color-main-brown);
    }
}

.hero {
    display: grid;
    grid-auto-flow: column;
    grid-template-columns: 1fr 4fr;
    gap: 48px;
}
</style>
