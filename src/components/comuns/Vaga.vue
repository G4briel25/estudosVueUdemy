<template>
    <div class="card">
        <div class="card-header bg-dark text-white">{{ props.titulo }}</div>
        <div class="card-body">
            <p>{{ props.descricao }}</p>
        </div>
        <div class="card-footer">
            <small class="text-muted">Salário: R$ {{ props.salario }} | Modalidade: {{ getModalidade }} | Tipo: {{
                getTipo }} | Publicação:
                {{ props.publicacao }}</small>
        </div>
    </div>
</template>

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
    modalidade: {
        type: String,
        required: true
    },
    tipo: {
        type: String,
        required: true
    },
    publicacao: {
        type: String,
        required: true
    }
});

const getModalidade = computed(() => {
    switch (props.modalidade) {
        case 1:
            return 'Home Office'
            break;
        case 2:
            return 'Presencial'
            break;
    }
    return '';
});

const getTipo = computed(() => {
    switch (props.tipo) {
        case 1:
            return 'CLT'
            break;
        case 2:
            return 'PJ'
            break;
    }
    return '';
});

</script>
