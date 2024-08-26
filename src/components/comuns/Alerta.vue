<script setup>
import { onMounted, defineProps, computed } from 'vue';


const props = defineProps({
    tipo: String
});

onMounted(() => {
    console.log('O tipo do alerta é:', props.tipo);
});

const estiloAlerta = computed(() => {
    switch (props.tipo) {
        case 'erro':
            return 'alert alert-danger'
        case 'sucesso':
            return 'alert alert-success'
        default:
            return 'alert alert-success';
    }
});

</script>

<template>
    <div :class="estiloAlerta" role="alert">
        <slot name="titulo">
            <h3>Título da mensagem de feedback</h3>
        </slot>
        <hr>
        <slot>
            <p>Mensagem de feedback</p>
        </slot>
    </div>
</template>
