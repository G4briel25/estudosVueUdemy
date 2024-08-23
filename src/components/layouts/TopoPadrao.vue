<script setup>
import { defineEmits, defineProps } from 'vue';

// const myEmit = defineEmits('emitParaComponentePai');

// const navegarPara = () => {
//     myEmit('emitParaComponentePai',
//         (p1, p2) => {
//             console.log('Função de callback pelo componente filho');
//             console.log('P1:', p1);
//             console.log('P2:', p2);
//         }
//     );
// }

const props = defineProps({
    funcaoCallback: {
        type: Function,
        required: true
    }
});

const handleClick = (param1, param2) => {
    props.funcaoCallback(param1, param2)
};


</script>


<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container">
            <a class="navbar-brand" href="#">Vagas</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false"
                aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                    <li class="nav-item">
                        <a class="nav-link" href="#" @click="handleClick('Teste1', 123)">Home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#" @click="handleClick('Teste2', 321)">Publicar Vaga</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>
