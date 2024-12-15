<script setup>
import { useForm, configure, useResetForm } from 'vee-validate'
import * as yup from 'yup'
import { reactive, ref } from 'vue';
import MessageComp from './MessageComp.vue';
const politic = ref(true)
const { errors, defineField, handleSubmit } = useForm({
    validationSchema: yup.object({
        name: yup.string().required('Необходимо ввести ваше имя'),
        tel: yup.string().matches(/^\+?\d{6,15}$/, 'Некорретный номер телефона'),
        email: yup.string().email().required(),
        city: yup.string().required(),
        street: yup.string().required(),
        building: yup.string().required(),
        flat: yup.number(),
        politics: yup.bool().required('Необходимо согласие на обработку персональных данных')
    })
})

configure({
    validateOnBlur: true,
    validateOnInput: false,
    validateOnModelUpdate: false,
});

const [name, nameAttrs] = defineField('name')
const [tel, telAttrs] = defineField('tel')
const [email, emailAttrs] = defineField('email')
const [comments, commentsAttrs] = defineField('comments')
const [country] = defineField('country')
const [city, cityAttrs] = defineField('city')
const [street, streetAttrs] = defineField('street')
const [building, buildingAttrs] = defineField('building')
const [flat, flatAttrs] = defineField('flat')
const [politics, politicsAttrs] = defineField('politics')
const completed = ref(false)
const msg = ref('empty')

const onSubmit = handleSubmit(values => {
    const order = { ...values, goods: { ...cart } }
    fetch('https://httpbin.org/anything', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(order)
    })
        .then(res => res.json())
        .then(completed.value = true,
            msg.value = "Спасибо! Заказ успешно оформлен! "
        )
        .catch(error => console.error('Ошибка:', error));

});

const coutries = reactive([
    {
        id: 1,
        country: 'Россия'
    },
    {
        id: 2,
        country: 'Белоруссия'
    },
    {
        id: 1,
        country: 'Казахстан'
    }
])
const cart = reactive([
    {
        name: 'Куртка',
        count: 2,
        price: 1234
    },
    {
        name: 'Шарф',
        count: 1,
        price: 141
    },
    {
        name: 'Шапка',
        count: 4,
        price: 134
    },
])
</script>
<template>
    <div class="wrapper">
        <div v-if="!completed" class="checkout">
            <form @submit="onSubmit">
                <div class="form-container">
                    <div class="form-header">Оформление заказа:</div>
                    <div class="form-fields">
                        <label for="name">Ваше имя:</label>
                        <input v-model="name" v-bind="nameAttrs" />
                        <div class="error_msg">{{ errors.name }}</div>
                    </div>
                    <div class="form-fields">
                        <label for="tel">Номер телефона: </label>
                        <input v-model="tel" v-bind="telAttrs" />
                        <div class="error_msg">{{ errors.tel }}</div>
                    </div>
                    <div class="form-fields">
                        <label for="email">Адрес электронной почты: </label>
                        <input v-model="email" v-bind="emailAttrs" />
                        <div class="error_msg">{{ errors.email }}</div>
                    </div>
                    <div class="form-fields">
                        Адрес доставки:
                    </div>
                    <div class="form-fields">
                        <div>
                            <label for="country">Страна:</label>
                            <select name="country" v-model="country">
                                <option selected disabled>Выбрать страну..</option>
                                <option v-for="i of coutries" :key="i.id">{{ i.country }}</option>
                            </select>
                        </div>
                        <div>
                            <label for="city">Город: </label>
                            <input v-model="city" v-bind="cityAttrs" />
                            <div class="error_msg">{{ errors.city }}</div>
                        </div>
                        <div>
                            <label for="street">Улица: </label>
                            <input v-model="street" v-bind="streetAttrs" />
                            <div class="error_msg">{{ errors.street }}</div>
                        </div>
                        <div>
                            <label for="building">Дом\строение: </label>
                            <input v-model="building" v-bind="buildingAttrs" />
                            <div class="error_msg">{{ errors.building }}</div>
                        </div>
                        <div>
                            <label for="flat">Квартира\офис: </label>
                            <input v-model="flat" v-bind="flatAttrs" />
                            <div class="error_msg">{{ errors.flat }}</div>
                        </div>

                    </div>
                    <div class="form-fields">
                        <label for="comments">Комментарии к заказу: </label>
                        <textarea v-model="comments" v-bind="commentsAttrs" />
                        <div class="error_msg">{{ errors.comments }}</div>
                    </div>
                    <div>
                        <input type="checkbox" v-model="politics" v-bind="politicsAttrs" @click="politic = !politic"
                            autocomplete="false">
                        Нажимая кнопку "Отправить", Вы даёте своё согласие на обработку введённой персональной
                        информации в соответствии с ФЗ№152-ФЗ "О персональных данных"
                        <div class="error_msg">{{ errors.politics }}</div>
                    </div>
                    <button :disabled="politic" :class="{ isActive: politic }" @click="onSubmit">Отправить</button>
                </div>
            </form>
            <div class="cart-items">

                <div>
                    <div><b>Ваш заказ</b></div>
                </div>
                <div v-for="el of cart" :key="el" class="cart-item">
                    <p><i>{{ el.name }}</i></p>
                    <div class="cart-item-price">
                        <div>{{ el.price }} x {{ el.count }}</div>
                        <div><b>{{ el.count * el.price }}</b></div>
                    </div>
                </div>
                <div class="cart-summ">
                    <div><b>Итого: </b></div>
                </div>

            </div>
        </div>
        <MessageComp v-if="completed" :msg="msg"></MessageComp>
    </div>
</template>
<style scoped>
.buttons-wrap {
    display: flex;
    flex-direction: row;
    width: fit-content;
}

.form-container {
    display: flex;
    flex-direction: column;
    gap: 15px;
    padding: 15px;
    width: 100%;
    justify-items: start;
    align-items: start;
    border-radius: 5px;
    box-shadow: 1px 2px 4px rgba(0, 0, 0, 0.1);
}

.form-header {
    font-size: 20px;
}

.form-fields {
    display: flex;
    flex-direction: column;
    justify-content: start;
    width: 80%;
    gap: 5px;
}

.form-fields input,
textarea,
select {
    font-size: 14px;
    height: 30px;
    border: 1px solid burlywood;
    border-radius: 7px;
}

textarea {
    height: 100px;
}

.form-container button {
    margin: 20px;
    background: #8fedda;
    border: none;
    color: rgb(2, 37, 62);
}

.isActive {
    opacity: 0.5;
}

.error_msg {
    color: brown;
    font-size: small;
}

.checkout {
    display: grid;
    grid-template-columns: auto 30%;
    gap: 20px;
}

.cart-items {
    box-shadow: 1px 2px 4px rgba(0, 0, 0, 0.1);
    padding: 10px;
}

.cart-item {
    display: flex;
    flex-direction: column;

}

.cart-item>div {
    border-bottom: 1px dashed;
}

.cart-item>p {
    margin-bottom: 0.1em;
}

.cart-item-price {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}

.cart-summ {
    float: right;
}
</style>