<template>
    <div class="done">
        <div class="msg">{{ props.msg }}</div>
    </div>
</template>
<script setup>
import { string } from 'yup';


const props = defineProps({ msg: string })
</script>
<style>
.done {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    font-size: large;
    margin: 0 auto;
    width: 100%;
    border-radius: 5px;
    box-shadow: 1px 2px 4px rgba(0, 0, 0, 0.1);
    min-height: 50vh;
}

.msg {
    width: fit-content;
    margin: 0 auto;
}
</style>