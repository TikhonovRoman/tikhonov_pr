<template>
    <header>
        <div>
            <div class="logo">MarketPlace</div>
            <ul class="header-menu">
                <li><a href="#">Контакты</a></li>
                <li><a href="#">Помощь</a></li>
                <li><a href="#">Доставка и оплата</a></li>
            </ul>
        </div>
    </header>
</template>
<style scoped>
.logo {
    font-size: 3em;
}

a {
    color: rgb(94, 94, 91);
}

.header-menu {
    display: flex;
    gap: 15px;
}

header div {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin-bottom: 1rem;
}
</style>