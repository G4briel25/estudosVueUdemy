<script setup>
import { onMounted, ref, getCurrentInstance } from "vue";
import TopoPadrao from "@/components/layouts/TopoPadrao.vue";
import Conteudo from "@/components/layouts/Conteudo.vue";
import VagasFavoritas from "@/components/comuns/VagasFavoritas.vue";
import Alerta from "@/components/comuns/Alerta.vue";

const component = ref('Home');


onMounted(() => {
  const instance = getCurrentInstance();
  const thisVue = instance.appContext.config.globalProperties;

  thisVue.emitter.on('alerta', () => {
    console.log('Mensagem de alerta aqui');
  });
});


</script>

<template>

  <Alerta></Alerta>

  <VagasFavoritas></VagasFavoritas>

  <TopoPadrao @navegar="component = $event"></TopoPadrao>

  <Conteudo :conteudo="component"></Conteudo>
</template>

<style></style>
