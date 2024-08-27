<script setup>
import { ref, getCurrentInstance } from 'vue';

const data = ref({
    titulo: '',
    descricao: '',
    salario: '',
    modalidade: null,
    tipo: null
});

const instance = getCurrentInstance();
const thisVue = instance.appContext.config.globalProperties;

const salvarVaga = () => {
    let tempoDecorrido = Date.now();
    let datAtual = new Date(tempoDecorrido);
    let dataPublicacao = datAtual.toISOString();

    let vagas = JSON.parse(localStorage.getItem('vagas'));

    if (!vagas) vagas = [];

    vagas.push({
        titulo: data.value.titulo,
        descricao: data.value.descricao,
        salario: data.value.salario,
        modalidade: data.value.modalidade,
        tipo: data.value.tipo,
        publicacao: dataPublicacao
    });

    if (validaFormulario()) {
        localStorage.setItem('vagas', JSON.stringify(vagas));

        thisVue.emitter.emit('alerta', {
            tipo: 'sucesso',
            titulo: `A vaga ${data.value.titulo} foi cadastrada com sucesso :)`,
            descricao: `Parabéns, a vaga foi cadastrada e poderá ser consultada por milhares de profissionais`
        });

        limparFormulario();

    } else {
        thisVue.emitter.emit('alerta', {
            tipo: 'erro',
            titulo: `Opss... Não foi possível realizar o cadastro.`,
            descricao: `É obrigatório preencher todos os campos!`
        });
    }
}

const limparFormulario = () => {
    data.value.titulo = '';
    data.value.descricao = '';
    data.value.salario = '';
    data.value.modalidade = null;
    data.value.tipo = null;
};

const validaFormulario = () => {
    let valido = true;

    if (data.value.titulo === '') valido = false;
    if (data.value.descricao === '') valido = false;
    if (data.value.salario === '') valido = false;
    if (data.value.modalidade === '') valido = false;
    if (data.value.tipo === '') valido = false;

    return valido;
};

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
                <select class="form-select" v-model.number="data.modalidade">
                    <option value="" selected disabled>--Selecione</option>
                    <option value="1">Home Office</option>
                    <option value="2">Presencial</option>
                </select>
                <div class="form-text">Informe o tipo de contratação.</div>
            </div>

            <div class="col">
                <label class="form-label">Tipo</label>
                <select class="form-select" v-model.number="data.tipo">
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