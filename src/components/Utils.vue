<script lang="ts">
import Paginacao from "@/components/Utils/Paginacao.vue";

export default { 
    data() {
        return {
            paginaAtual: 1, 
            multiplicador: 1,
        }
    },
    components: {
        Paginacao
    },
    methods: {
        childRetornaPagiancao(paginacaoRetorno , multiplicador) {
            this.paginaAtual = paginacaoRetorno;
            this.multiplicador = multiplicador;
        }
    }
}
</script>
<template>
    <h1>Utils</h1>
    <Paginacao :quantidade="50" 
    :multiplicador="5" 
    @retornaPaginacao="childRetornaPagiancao"
    :limitePaginacao="6" 
    :travarPaginacao="false"
    ></Paginacao>


    {{ paginaAtual  }}{{ multiplicador }}
</template>