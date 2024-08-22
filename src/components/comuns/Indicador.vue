<script setup>
import { computed, defineProps } from 'vue';

const props = defineProps({
    titulo: String,
    indicador: [Number, String, Object],
    bg: String,
    color: String
});

const estilo = computed(() => {
    return `h-100 p-5 rounded-3 border ${props.bg} ${props.color}`;
})

</script>

<template>
    <div :class="estilo">
        <p>{{ props.titulo }}</p>
        <h2>{{ props.indicador }}</h2>
    </div>
</template>