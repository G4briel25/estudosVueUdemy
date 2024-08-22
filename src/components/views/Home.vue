<script setup>
import { onActivated, onBeforeUnmount, onDeactivated, onMounted, onUnmounted } from "vue";
import PesquisarVaga from "../comuns/PesquisarVaga.vue";
import Indicador from "../comuns/Indicador.vue";

onMounted(() => {
    console.log('Componente é montado')
})

onActivated(() => {
    console.log('Componente é ativado')
});

onDeactivated(() => {
    console.log('Componente desativado')
});

onBeforeUnmount(() => {
    console.log('Antes de desmontar/destruir');
});

onUnmounted(() => {
    console.log('Desmontado/destruído');
});

</script>

<template>
    <div class="container py-4">
        <div class="row">
            <div class="col">
                <PesquisarVaga />
            </div>
        </div>

        <div class="row mt-5">
            <div class="col-4">
                <Indicador />
            </div>

            <div class="col-4">
                <Indicador />
            </div>

            <div class="col-4">
                <Indicador />
            </div>
        </div>
    </div>
</template>
