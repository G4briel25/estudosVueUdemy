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

<<<<<<< HEAD
=======
const acao = (p1, p2) => {
  console.log('Função de callback definida no componente Pai e chamada no componte Filho');
  console.log('P1', p1);
  console.log('P2', p2)
}
>>>>>>> 24c6787e489fb5aa456c8707dd75c306a27e1f8a

</script>

<template>

  <Alerta></Alerta>

  <VagasFavoritas></VagasFavoritas>

  <TopoPadrao @navegar="component = $event"></TopoPadrao>

  <Conteudo :conteudo="component"></Conteudo>
</template>

<style></style>
