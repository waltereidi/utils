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
            showModalImagem : false , 
            
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
        },
         childFecharModalImagem() {
            this.showModalImagem = false;
        }
    }, 
   
}
</script>
<template>
    <h1>Utils-Paginacao</h1>
    <Paginacao 
        :quantidade="50" 
        :multiplicador="5" 
        @retornaPaginacao="childRetornaPagiancao"
        :limitePaginacao="6" 
        :travarPaginacao="false">
    </Paginacao>

<h1>Utils-ModalImagem</h1>
<img :src="configDataSource.capaLivroDefault" @click="showModalImagem=true" style="height: 50px;">
    <ModalImagem 
        :srcImagem="configDataSource.capaLivroDefault" 
        :showModal="showModalImagem"
        @fecharModal="childFecharModalImagem">
    </ModalImagem>
</template>