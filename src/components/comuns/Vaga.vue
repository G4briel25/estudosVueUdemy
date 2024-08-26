<script setup>
import { computed, defineProps, getCurrentInstance, ref, watch } from 'vue';

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


const instancia = getCurrentInstance();
const thisVue = instancia.appContext.config.globalProperties;
const favoritada = ref(false);

watch(favoritada, (novoValor) => {
    if (novoValor) {
        thisVue.emitter.emit('favoritarVaga', props.titulo);
    } else {
        thisVue.emitter.emit('desfavoritarVaga', props.titulo);
    }
});

</script>

<template>
    <div class="card">
        <div class="card-header bg-dark text-white">
            <div class="row">
                <div class="col d-flex justify-content-between">
                    <div>
                        {{ props.titulo }}
                    </div>
                    <div>
                        <div class="form-check form-switch">
                            <input class="form-check-input" type="checkbox" v-model="favoritada">
                            <label class="form-check-label">Favoritar / {{ favoritada }}</label>
                        </div>
                    </div>
                </div>
            </div>
        </div>
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
