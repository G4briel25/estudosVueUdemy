<script setup>
import { onMounted, ref, getCurrentInstance } from "vue";
import TopoPadrao from "@/components/layouts/TopoPadrao.vue";
import Conteudo from "@/components/layouts/Conteudo.vue";
import VagasFavoritas from "@/components/comuns/VagasFavoritas.vue";
import Alerta from "@/components/comuns/Alerta.vue";

const component = ref('Home');

const alerta = ref({
  titulo: '',
  descricao: '',
  tipo: ''
});

const exibirAlerta = ref(false);

onMounted(() => {
  const instance = getCurrentInstance();
  const thisVue = instance.appContext.config.globalProperties;

  thisVue.emitter.on('alerta', (a) => {
    alerta.value = a;

    console.log(alerta.value);

    exibirAlerta.value = true;
    setTimeout(() => {
      exibirAlerta.value = false
    }, 5000);
  });
});

</script>

<template>

  <VagasFavoritas></VagasFavoritas>

  <TopoPadrao @navegar="component = $event"></TopoPadrao>

  <Alerta v-if="exibirAlerta" :tipo="alerta.tipo">
    <template v-slot:titulo>
      <h5>{{ alerta.titulo }}</h5>
    </template>
    <p>{{ alerta.descricao }}</p>
  </Alerta>

  <Conteudo :conteudo="component"></Conteudo>
</template>

<style></style>
