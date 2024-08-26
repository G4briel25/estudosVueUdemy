<script setup>
import Home from '@/components/views/Home.vue';
import PublicarVaga from '@/components/views/PublicarVaga.vue';


const componentes = {
    Home,
    PublicarVaga
}
defineProps({
    conteudo: {
        type: String,
        required: true
    }
});

</script>

<template>
    <keep-alive>
        <component :is="componentes[conteudo]"></component>
    </keep-alive>
</template>

<style scoped></style>