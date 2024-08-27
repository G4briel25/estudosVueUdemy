<script setup>
import { ref, onMounted, getCurrentInstance } from 'vue';

const instance = getCurrentInstance();
const thisVue = instance.appContext.config.globalProperties

onMounted(() => {
    thisVue.emitter.on('favoritarVaga', (titulo) => {
        vagas.value.push(titulo);
    });

    thisVue.emitter.on('desfavoritarVaga', (titulo) => {
        let indiceArray = vagas.value.indexOf(titulo);
        if (indiceArray !== -1) vagas.value.splice(indiceArray, 1);
    });
});

const vagas = ref([]);

</script>


<template>
    <div class="divVagaFavoritas">
        <button class="btn btn-primary" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasRight"
            aria-controls="offcanvasRight">Vagas Favoritadas</button>
    </div>

    <div class="offcanvas offcanvas-end" tabindex="-1" id="offcanvasRight" aria-labelledby="offcanvasRightLabel">
        <div class="offcanvas-header">
            <h5 class="offcanvas-title" id="offcanvasRightLabel">Vagas Favoritadas</h5>
            <button type="button" class="btn-close" data-bs-dismiss="offcanvas" aria-label="Close"></button>
        </div>
        <div class="offcanvas-body">
            <ul class="list-group" v-for="(vaga, index) in vagas" :key="index">
                <li class="list-group-item">{{ vaga }}</li>
            </ul>
        </div>
    </div>
</template>

<style scoped>
.divVagaFavoritas {
    position: absolute;
    z-index: 1;
    top: 10px;
    right: 5px;
}
</style>