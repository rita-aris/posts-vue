<template>
  <nav>
    <RouterLink to="/" exact-active-class="active">Главная</RouterLink>
    <RouterLink to="/posts" exact-active-class="active">Посты</RouterLink>
    <RouterLink to="/about" exact-active-class="active">О приложении</RouterLink>
  </nav>
</template>

<script>
export default {

}
</script>

<style scoped>
nav {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 30px;
}
nav a {
  font-size: 12px;
  text-decoration: none;
  &:hover {
    opacity: 0.7;
  }
  &.active {
    text-decoration: underline;
  }
}
</style>