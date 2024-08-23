<script setup>
import { computed, defineProps } from 'vue';

const props = defineProps({
    titulo: {
        type: String,
        required: true,
        // validator(p) {
        //     console.log(p);
        // }
    },
    descricao: {
        type: String,
        default: 'O contratante não adicionou uma descrição para essa vaga'
    },
    salario: {
        type: Number,
        required: true
    },
    modalidade: Number,
    tipo: Number,
    publicacao: {
        type: String,
        required: true
    }
});

const getModalidade = computed(() => {
    switch (props.modalidade) {
        case 1:
            return 'Home Office'
        case 2:
            return 'Presencial'
        default:
            return 'Não especificado';
    }
});

const getTipo = computed(() => {
    switch (props.tipo) {
        case 1:
            return 'CLT'
        case 2:
            return 'PJ'
        default:
            return 'Não especificado';
    }
});

const getPublicacao = computed(() => {
    let dataPublicacao = new Date(props.publicacao)
    return dataPublicacao.toLocaleDateString('pt-BR');
});

</script>

<template>
    <div class="card">
        <div class="card-header bg-dark text-white">{{ props.titulo }}</div>
        <div class="card-body">
            <p>{{ props.descricao }}</p>
        </div>
        <div class="card-footer">
            <small class="text-muted">Salário: R$ {{ props.salario }} | Modalidade: {{ getModalidade }} | Tipo: {{
                getTipo }} | Publicação:
                {{ getPublicacao }}</small>
        </div>
    </div>
</template>
