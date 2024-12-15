<template>

  <DefaultLayout>
    <template #header>
      <Header></Header>
    </template>
    <template #navigation>
      <Navigation @set-page="page = $event" @search-input="searchActive($event)"></Navigation>
    </template>
    <template #default>
      <Catalog v-if="page == 'Catalog'" :searchVal="searchValue"></Catalog>
      <Checkout @page="page = $event" v-if="page === 'Checkout'"></Checkout>
      <AddGoods v-if="page === 'AddGoods'"></AddGoods>
    </template>
    <template #footer>
      <Footer></Footer>
    </template>

  </DefaultLayout>
</template>

<script setup>
import DefaultLayout from '@/Layout/DefaultLayout.vue';
import Header from '@/components/Header.vue';
import AddGoods from '@/components/AddGoods.vue';
import Catalog from '@/components/Catalog.vue';
import Checkout from '@/components/Checkout.vue';
import Navigation from '@/components/Navigation.vue';
import Footer from '@/components/Footer.vue';
import { ref } from 'vue';

const page = ref('Catalog')
const searchValue = ref('')
function searchActive(e){
  searchValue.value=e
  page.value='Catalog'
}
</script>

<style scoped>
.aside {
  min-width: 300px;
  border: 1px solid chocolate;
}
</style>
