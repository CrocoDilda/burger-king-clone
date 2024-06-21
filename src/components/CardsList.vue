<script setup>
import Card from './card-components/Card.vue'

defineProps({
    itemsList: Array,
    tabState: Number
})
</script>

<template>
    <div v-auto-animate class="wrapper">
        <h2 class="title">Новинки</h2>
        <ul class="cards-list">
            <Card
                v-for="item in itemsList"
                :key="item.itemId"
                :itemId="item.itemId"
                :itemName="item.itemName"
                :itemPrice="item.itemPrice"
                :itemImageUrl="item.itemImageUrl"
                :itemType="item.itemType"
                :tabState="tabState"
            />
        </ul>
    </div>
</template>

<style scoped>
.wrapper {
    &:focus-visible {
        outline: 0px solid var(--color-main-brown);
    }
}

.title {
    font-size: 3.75rem;
    color: var(--color-main-brown);
    font-weight: 700;
    background-color: var(--color-bg-white100);
    padding: 32px 0 20px 15px;
    position: sticky;
    top: 80px;
    margin-left: -15px;
    width: 105%;
    z-index: 3;
    line-height: 3.75rem;
}

.cards-list {
    display: grid;
    grid-template-columns: repeat(3, auto);
    grid-template-rows: repeat(auto-fit, minmax(300px, 1fr));
    gap: 30px;
    margin-top: 40px;
    padding-bottom: 5px;
}
</style>
