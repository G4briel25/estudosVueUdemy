<script setup>
import TopoPadrao from "@/components/layouts/TopoPadrao.vue";
import Conteudo from "@/components/layouts/Conteudo.vue";

const acao = (p1, p2) => {
  console.log('Função de callback definida no componente Pai e chamada no componte Filho');
  console.log('P1', p1);
  console.log('P2', p2)
}

</script>

<template>
  <TopoPadrao :funcaoCallback="acao"></TopoPadrao>

  <Conteudo></Conteudo>

</template>

<style></style>
