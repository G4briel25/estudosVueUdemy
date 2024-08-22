<script setup>
import { ref } from 'vue';

const data = ref({
    titulo: '',
    descricao: '',
    salario: '',
    modalidades: '',
    tipo: ''
});

const salvarVaga = () => {
    let vagas = JSON.parse(localStorage.getItem('vagas'));
    console.log(vagas)

    if (!vagas) vagas = [];

    vagas.push({
        titulo: data.value.titulo,
        descricao: data.value.descricao,
        salario: data.value.salario,
        modalidades: data.value.modalidades,
        tipo: data.value.tipo
    });

    localStorage.setItem('vagas', JSON.stringify(vagas));
}
</script>

<template>
    <div class="container py-4">
        <div class="row">
            <div class="col">
                <h4>Apresente a sua vaga para milhares de profissionais e de graça</h4>
            </div>
        </div>

        <div class="row mt-3">
            <div class="col">
                <label class="form-label">Título da Vaga</label>
                <input type="text" class="form-control" v-model="data.titulo">
                <div class="form-text">Por exemplo: Programador JavaScript e VueJS.</div>
            </div>
        </div>

        <div class="row mt-3">
            <div class="col">
                <label class="form-label">Descrição</label>
                <textarea type="text" class="form-control" v-model="data.descricao"></textarea>
                <div class="form-text">Informe os detalhes da vaga.</div>
            </div>
        </div>

        <div class="row mt-3">
            <div class="col">
                <label class="form-label">Salário</label>
                <input type="number" class="form-control" v-model="data.salario">
                <div class="form-text">Informe o salário.</div>
            </div>

            <div class="col">
                <label class="form-label">Modalidade</label>
                <select class="form-select" v-model="data.modalidades">
                    <option value="" selected disabled>--Selecione</option>
                    <option value="1">Home Office</option>
                    <option value="2">Presencial</option>
                </select>
                <div class="form-text">Informe onde as atividades serão realizadas.</div>
            </div>

            <div class="col">
                <label class="form-label">Tipo</label>
                <select class="form-select" v-model="data.tipo">
                    <option value="" selected disabled>--Selecione</option>
                    <option value="1">CLT</option>
                    <option value="2">PJ</option>
                </select>
                <div class="form-text">Informe o tipo de contratação.</div>
            </div>
        </div>

        <div class="row mt-3">
            <div class="col">
                <button type="submit" class="btn btn-primary" @click="salvarVaga()">Cadastrar</button>
            </div>
        </div>

    </div>
</template>

<style></style>