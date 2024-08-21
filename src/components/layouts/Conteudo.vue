<script setup>
import {
    ref,
    onBeforeMount,
    onBeforeUnmount,
    onBeforeUpdate,
    onMounted,
    onUpdated,
    onUnmounted,
    onErrorCaptured,
    onRenderTracked,
    onRenderTriggered,
    onActivated,
    onDeactivated
} from 'vue';
import Home from '@/components/views/Home.vue';
import PublicarVaga from '@/components/views/PublicarVaga.vue';


const myMessage = ref('Minha mensagem aqui');

const showMessage = () => {
    alert(myMessage.value);
}

const titulo = ref('');
const atualizarComponente = () => {
    titulo.value += '*';
};


const visible = ref(true);
const desmontarComponente = () => {
    visible.value = false;
}

const componentes = {
    Home,
    PublicarVaga
}
const conteudo = ref('Home');

// Lifecycle Hooks
onBeforeMount(showMessage);

onMounted(showMessage);

onBeforeUpdate(() => {
    console.log('Antes de atualizar')
});

onUpdated(() => {
    console.log('Atualizado')
});

/*
onErrorCaptured(() => {
    console.log('Erro capturado')
});

onRenderTracked(() => {
    console.log('Re-renderização rastreada')
});

onRenderTriggered(() => {
    console.log('Re-renderização acionada')
});

onActivated(() => {
    console.log('Componente é ativado')
});

onDeactivated(() => {
    console.log('Componente desativado')
});
*/

</script>

<template>
    <h1>{{ titulo }}</h1>
    <button class="btn btn-secondary" @click="atualizarComponente()">Atualizar</button>
    <!-- <Home />
    <PublicarVaga v-if="visible" /> -->
    <button class="btn btn-warning" @click="desmontarComponente()">Desmontar Componente</button><br><br>
    <button class="btn btn-success" @click="conteudo = 'Home'">Home</button>
    <button class="btn btn-primary" @click="conteudo = 'PublicarVaga'">Publicar Vaga</button>
    <component :is="componentes[conteudo]"></component>
</template>

<style scoped></style>