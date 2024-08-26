<script setup>
import { ref, onMounted, onActivated, getCurrentInstance } from "vue";
import PesquisarVaga from "@/components/comuns/PesquisarVaga.vue";
import Indicador from "@/components/comuns/Indicador.vue";
import Vaga from "@/components/comuns/Vaga.vue";


const usuariosOnline = ref(0);

const getUsuariosOnline = () => {
    usuariosOnline.value = Math.floor(Math.random() * 101);
    return usuariosOnline;
}

onMounted(() => {
    setInterval(getUsuariosOnline, 2000);

    const instance = getCurrentInstance();
    const thisVue = instance.appContext.config.globalProperties;

    thisVue.emitter.on('filtrarVagas', vaga => {
        console.log('Estamos no componente HOME', vaga);
    })
});

const vagas = ref([]);

onActivated(() => {
    vagas.value = JSON.parse(localStorage.getItem('vagas'));
});

</script>

<template>
    <div class="container py-4">
        <div class="row">
            <div class="col">
                <PesquisarVaga />
            </div>
        </div>

        <div class="row mt-5" v-for="(vaga, index) in vagas" :key="index">
            <div class="col">
                <Vaga :titulo="vaga.titulo" :descricao="vaga.descricao" :salario="vaga.salario"
                    :modalidade="vaga.modalidade" :tipo="vaga.tipo" :publicacao="vaga.publicacao" />
            </div>
        </div>

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
