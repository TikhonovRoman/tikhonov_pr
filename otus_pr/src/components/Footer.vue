<template>
  <div class="footer">
    <ul>
      <li><a href="#">Главная</a></li>
      <li><a href="#">О нас</a></li>
      <li><a href="#">Контакты</a></li>
      <li><a href="#">Каталог</a></li>
    </ul>
    <div class="rights">Все права защищены</div>
  </div>
</template>
<style scoped>
.footer {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  width: 100%;
  background: gray;
  border-radius: 5px;
  margin-top: 2em;
  padding: 20px;
}

li {
  display: block;
  list-style: none;
}

a {
  text-decoration: none;
  color: antiquewhite;
}

.rights {
  align-self: end;
  justify-self: center;
}
</style>
