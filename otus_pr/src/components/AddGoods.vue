<template>

    <form v-if="!completed" @submit="onSubmit">
        <div class="form-container">
            <div class="form-header">Добавление нового товара в каталог:</div>
            <div class="form-fields">
                <label for="title">Название: </label>
                <input v-model="title" v-bind="titleAttrs" />
                <div class="error_msg">{{ errors.title }}</div>
            </div>
            <div class="form-fields">
                <label for="price">Цена: </label>
                <input v-model="price" v-bind="priceAttrs" />
                <div class="error_msg">{{ errors.price }}</div>
            </div>
            <div class="form-fields">
                <label for="discription">Описание: </label>
                <input v-model="discription" v-bind="discriptionAttrs" />
                <div class="error_msg">{{ errors.discription }}</div>
            </div>
            <div class="form-fields">
                <label for="img">Категория: </label>
                <input v-model="category" v-bind="categoryAttrs" />
                <div class="error_msg">{{ errors.category }}</div>
            </div>
            <div class="form-fields">
                <label for="img">Изображение: </label>
                <input v-model="img" v-bind="imgAttrs" />
                <div class="error_msg">{{ errors.img }}</div>
            </div>
            <button @click="onSubmit">Добавить</button>
        </div>
    </form>
    <MessageComp v-if="completed" :msg="msg"></MessageComp>
</template>
<script setup>
import { useForm } from 'vee-validate'
import * as yup from 'yup'
import { ref } from 'vue';
import MessageComp from './MessageComp.vue';

const completed = ref(false)
const msg = ref('empty')
const newProduct = ref()
const { errors, defineField, handleSubmit } = useForm({
    validationSchema: yup.object({
        title: yup.string().min(6).required(),
        price: yup.number().positive().required().max(100000000),
        discription: yup.string().min(20).required(),
        category: yup.string().required(),
        img: yup.string()

    })
})
const onSubmit = handleSubmit(values => {
    alert(JSON.stringify(values, null, 2));
    const newProduct = values
    fetch('https://fakestoreapi.com/products', {
        method: 'POST',
        body: JSON.stringify(newProduct)
    })
        .then(res => res.json())
        .then(completed.value = true,
            msg.value = "Товар добавлен в каталог",
        )
        .catch(error => console.error('Ошибка:', error));

});
const [title, titleAttrs] = defineField('title')
const [price, priceAttrs] = defineField('price')
const [discription, discriptionAttrs] = defineField('discription')
const [category, categoryAttrs] = defineField('category')
const [img, imgAttrs] = defineField('img')


</script>
<style scoped>
.form-container {
    display: flex;
    flex-direction: column;
    gap: 15px;
    width: 100%;
    justify-items: center;
    align-items: center;
}

.form-header {
    font-size: 20px;
}

.form-fields {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 50%;
}

.form-fields input {
    width: 100%;
    height: 30px;
    font-size: large;
    border: 1px solid burlywood;
    border-radius: 10px;
}

.form-container button {
    width: 250px;
    margin: 20px;
    background: #8fedda;
    border: none;
    color: rgb(2, 37, 62);
}

.error_msg {
    color: brown;
    font-size: small;
}
</style>