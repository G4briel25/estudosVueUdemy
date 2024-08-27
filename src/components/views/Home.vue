<script setup>
import { ref, onMounted } from "vue";
import PesquisarVaga from "@/components/comuns/PesquisarVaga.vue";
import Indicador from "@/components/comuns/Indicador.vue";
import ListaVagas from "@/components/comuns/ListaVagas.vue";



const usuariosOnline = ref(0);

const getUsuariosOnline = () => {
    usuariosOnline.value = Math.floor(Math.random() * 101);
    return usuariosOnline;
}

onMounted(() => {
    setInterval(getUsuariosOnline, 2000);
});

</script>

<template>
    <div class="container py-4">
        <div class="row">
            <div class="col">
                <PesquisarVaga />
            </div>
        </div>

        <!-- <ListaVagas>
            <template v-slot:titulo="slotProps">
                {{ slotProps.dadosTitulo.titulo }}
                <hr>
            </template>
<template v-slot:default="slotProps">
                {{ slotProps.vagas }}
                <hr>
            </template>

<template v-slot:rodape="slotProps">
                {{ slotProps.dadosRodape.titulo }}
            </template>
</ListaVagas> -->

        <ListaVagas></ListaVagas>

        <div class="row mt-5">
            <div class="col-4">
                <Indicador titulo="Vagas abertas" indicador="100" bg="bg-light" color="text-dark" />
            </div>

            <div class="col-4">
                <Indicador titulo="Profissionais cadastrados" indicador="225" bg="bg-dark" color="text-white" />
            </div>

            <div class="col-4">
                <Indicador titulo="Visitantes online" :indicador="getUsuariosOnline()" bg="bg-light"
                    color="text-dark" />
            </div>
        </div>
    </div>
</template>
