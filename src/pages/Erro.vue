<template>
  <div id="erro">
    <img src="../assets/images/error/not_found.gif" alt="" />
    <h1>Página não encontrada.</h1>
    <br />
    <router-link to="/">Voltar para Home</router-link>
  </div>
</template>

<script>
export default {
  name: "Erro",
};
</script>

<style scoped>
#erro {
  display: flex;
  flex-direction: column;
  align-items: center;
}
img {
  width: 100px;
  height: 100px;
}
</style>