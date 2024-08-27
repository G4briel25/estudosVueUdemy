<script setup>
import Vaga from "@/components/comuns/Vaga.vue";
import { ref, getCurrentInstance, onMounted, onActivated } from "vue";


const vagas = ref([]);

onMounted(() => {

    const instance = getCurrentInstance();
    const thisVue = instance.appContext.config.globalProperties;

    thisVue.emitter.on('filtrarVagas', vaga => {

        const vagas1 = JSON.parse(localStorage.getItem('vagas'));
        vagas.value = vagas1.filter(reg => reg.titulo.toLowerCase().includes(vaga.titulo.toLowerCase()));

    });
});

onActivated(() => {
    vagas.value = JSON.parse(localStorage.getItem('vagas'));
});

</script>

<template>

    <slot name="titulo" :dadosTitulo="{ titulo: 'Título Lista', numeroVagas: 15 }"></slot>

    <slot :vagas="vagas">
        <div class="row mt-5" v-for="(vaga, index) in vagas" :key="index">
            <div class="col">
                <Vaga :titulo="vaga.titulo" :descricao="vaga.descricao" :salario="vaga.salario"
                    :modalidade="vaga.modalidade" :tipo="vaga.tipo" :publicacao="vaga.publicacao" />
            </div>
        </div>
    </slot>

    <slot name="rodape" :dadosRodape="{ titulo: 'Rodapé lista', paginacao: { numeroPaginas: 10, paginaAtual: 5 } }">
    </slot>

</template>
