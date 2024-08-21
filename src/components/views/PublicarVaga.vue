<script setup>
import { onBeforeUnmount, onUnmounted } from 'vue';

onBeforeUnmount(() => {
    console.log('PublicarVaga: Antes de destruir');
});

setTimeout(() => {
    console.log('PublicarVaga: 3 segundos depois');
}, 3000)

onUnmounted(() => {
    console.log('PublicarVagas: Destruído');
});
</script>

<template>
    <div>
        <h3>publicar vaga</h3>
    </div>
</template>

<style></style>