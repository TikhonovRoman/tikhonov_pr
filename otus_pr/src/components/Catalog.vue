<template>
    <div class="container">
        <Loader v-if="isLoading" />
        <div class="catalog" v-else>
            <div class="sort">
                <form class="sort-form">
                    <label for="price">Сортировать по цене:</label>
                    <div>
                        <input v-model.trim.lazy="prices.price1" type="number" placeholder="от 10" />
                        <input v-model.trim.lazy="prices.price2" type="number" placeholder="до 9990" />
                    </div>
                    <button @click="reset()">Сбросить</button>
                </form>
            </div>
            <div>

                <div class="goods">
                    <ICard v-for="product of filteredGoods" :key="product.id" :product="product"></ICard>
                </div>
            </div>
        </div>
    </div>

</template>
<script setup>
import { computed, onMounted, reactive, ref } from 'vue';
import ICard from '@/components/Card.vue';
import Loader from '@/Layout/Loader.vue';

const props = defineProps({ searchVal: '' })
const products = ref([])

const isLoading = ref(true)
const prices = reactive({
    price1: '',
    price2: ''
})
function reset() {
    Object.assign(prices, {
        price1: '',
        price2: ''
    })
}
onMounted(async () => {
    const res = await fetch('https://fakestoreapi.com/products')
    if (res.ok) {
        products.value = await res.json();
        setTimeout(() => {
            isLoading.value = false
        }, "100");
    } else {
        alert("Ошибка: " + res.status);
    }
})

const filteredGoods = computed(() => {
    let query = props.searchVal
    let goods = products.value

    if (query) {
        goods = goods.filter(item =>
            item.title.toLowerCase().includes(query.toLowerCase())
        )
    }
    if (prices.price1) {
        goods = goods.filter(item =>
            item.price >= prices.price1
        )
    }
    if (prices.price2) {
        goods = goods.filter(item =>
            item.price <= prices.price2
        )
    }

    return goods
})


</script>
<style scoped>
.container {
    display: flex;
    justify-content: center;
    align-items: center;
}

.catalog {
    display: grid;
    grid-template-columns: 25% auto;
    width: 100%;
    gap: 2em;
}

.sort {
    position: relative;
    margin-top: 20px;
}

.sort-form {
    position: sticky;
    top: 50px;
    display: flex;
    flex-direction: column;
    padding: 10px;
}

.sort-form div {
    display: flex;
    gap: 15px;
}

.sort-form input {
    width: 100%;
    height: 42px;
    font-size: 16px;
    padding-left: 10px;
    border: none;
    border-bottom: 2px solid gray;
    outline: none;
    background: #ffffff;
    color: #333131;
    margin-bottom: 20px;
}

button {
    background: #e1d2d2;
    color: #333131;
}

.goods {
    display: grid;
    grid-template-columns: repeat(auto-fill, 225px);
    justify-content: stretch;
    flex-flow: wrap;
    gap: 30px;
}
</style>