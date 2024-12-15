<template>

    <form @submit="$emit('searchInput', searchValue)">
      <input v-model="searchValue" type="search" placeholder="Поиск по названию..">
      <button @click="$emit('searchInput', searchValue)" type="submit">&#128269;</button>
    </form>

</template>
<script setup>
import { ref } from 'vue';

const searchValue = ref()
</script>
<style scoped>

form {
  display: flex;
  align-items: center;
  width: 70%;
}

input {
  width: 100%;
  height: 42px;
  padding-left: 10px;
  border: 1px solid gray;
  margin-right: -3px;
  border-radius: 5px;
  outline: none;
  background: #f8f6f0;
  color: #9E9C9C;
}

button {
  color: #F9F0DA;
  width: fit-content;
  height: 42px;
  border: 1px solid gray;
  border-left: none;
  background:#f8f6f0;
  border-radius: 0 5px 5px 0;
  cursor: pointer;
}
</style>