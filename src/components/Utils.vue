<script lang="ts">
import Paginacao from "@/components/Utils/Paginacao.vue";
import Config from "@/assets/json/bibliotecaconfig.json";
import ModalImagem from "@/components/Utils/ModalImagem.vue";

export default { 
    data() {
        return {
            paginaAtual: 1, 
            multiplicador: 1,
            configDataSource: Config,
            
        }
    },
    components: {
        Paginacao,
        ModalImagem
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
    <Paginacao 
        :quantidade="50" 
        :multiplicador="5" 
        @retornaPaginacao="childRetornaPagiancao"
        :limitePaginacao="6" 
        :travarPaginacao="false">
    </Paginacao>


    <ModalImagem 
        :srcImagem="configDataSource.capaLivroDefault" 
        :heightModal="'50'"
        :widthModal="'50'"
        :medida="'px'"
        ></ModalImagem>
</template>