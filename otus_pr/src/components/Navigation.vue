<template>
    <div class="nav-items">
        <ul>
            <li><a href="#" @click="$emit('set-page', 'Catalog')">Каталог</a></li>
            <InputSearch @search-input="$emit('searchInput', $event)"></InputSearch>
            <li><a href="#" @click="$emit('set-page', 'AddGoods')">Войти</a></li>
            <li><a href="#">Избранное</a></li>
            <li><a href="#" @click="$emit('set-page', 'Checkout')">Корзина</a></li>
        </ul>

    </div>
</template>
<script setup>
import InputSearch from '@/ui/InputSearch.vue';
</script>
<style scoped>
.nav-items {
    display: flex;
    gap: 15px;
    width: 100%;
    border-radius: 5px;
    justify-content: space-between;
}

ul {
    display: flex;
    margin: 0;
    padding: 0;
    width: 100%;
    gap: 15px;
}

.nav-items li {
    display: block;
    padding: 10px 25px;
    list-style: none;
    background: #9ce35f;
    border-radius: 5px;
    color: white;
}

.nav-items a {
    text-decoration: none;
    color: rgb(247, 247, 247);
}

.nav-items li:hover {
    background: green;
}
</style>