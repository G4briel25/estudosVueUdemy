<script setup>
import { ref, getCurrentInstance } from 'vue';


const titulo = ref('');

const instance = getCurrentInstance();
const thisVue = instance.appContext.config.globalProperties;

const filtrarVaga = () => {
    thisVue.emitter.emit('filtrarVagas', { titulo: titulo.value })
}
</script>

<template>
    <div class="h-100 p-5 bg-light border rounded-3">
        <h2>Pesquisar Vagas</h2>
        <div class="row">
            <div class="col">
                <div class="form-group">
                    <label>Título da vaga</label>
                    <input type="text" class="form-control"
                        placeholder="Pesquise por palavras chaves, por exemplo 'PHP', 'Pleno', 'Analista'"
                        v-model="titulo">
                    <small class="form-text text-muted">Informe palavras que estejam relacionadas com o
                        título da vaga que você procura</small>
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <button class="btn btn-outline-dark mt-2" type="button" @click="filtrarVaga">Buscar</button>
            </div>
        </div>
    </div>
</template>