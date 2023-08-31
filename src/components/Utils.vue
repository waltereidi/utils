<script lang="ts">
import Paginacao from "@/components/Utils/Paginacao.vue";
import Config from "@/assets/json/bibliotecaconfig.json";
import ModalImagem from "@/components/Utils/ModalImagem.vue";
import ModalFormulario from "@/components/Utils/ModalFormulario.vue";

export default { 
    data() {
        return {
            paginaAtual: 1, 
            multiplicador: 1,
            configDataSource: Config,
            showModalImagem : false , 
            showModalFormulario: {
                status: 0, 
                message: '' , 
            }, 
            
        }
    },
    components: {
        Paginacao,
        ModalImagem,
        ModalFormulario, 
    },
    methods: {
        childRetornaPagiancao(paginacaoRetorno , multiplicador) {
            this.paginaAtual = paginacaoRetorno;
            this.multiplicador = multiplicador;
        },
        
        childRetornaDataSourceFormulario( dataSource) {
            if (dataSource.nome === 'teste') {
                this.showModalFormulario.status = 200; 
                this.showModalFormulario.message = 'OK';
            };  
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

    <ModalImagem :srcImagem="configDataSource.capaLivroDefault" ></ModalImagem>

    <h1>Utils-ModalFormulario</h1>
        <ModalFormulario
            :resposta="showModalFormulario"
            @retornaDataSource="childRetornaDataSourceFormulario">
        </ModalFormulario>
</template>

