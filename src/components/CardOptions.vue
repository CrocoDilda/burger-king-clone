<script setup>
// Добавить в бг фильтр
//  @click="() => emit('popUpFunction')"
</script>

<template>
    <div class="wrapper">
        <div class="bg-filter"></div>
        <div class="options">
            <div class="title-block"></div>
            <ul class="modifications">
                <li class="modifications--item">
                    <button class="modifications--button"></button>
                </li>
            </ul>
        </div>
    </div>
</template>

<style scoped>
.wrapper {
    position: fixed;
    z-index: 99;
}
</style>
