<script lang="ts">

import Paginacao from "@/components/Utils/Paginacao.vue";
import Config from "@/assets/json/bibliotecaconfig.json";
import ModalImagem from "@/components/Utils/ModalImagem.vue";
import ModalFormulario from "@/components/Utils/ModalFormulario/ModalFormulario.vue";
import ModalContainer from "@/components/Utils/ModalContainer/ModalContainer.vue";
import GridContainer from "@/components/Utils/DataGrid/GridContainer.vue"; 

export default { 
    data() {
        return {
            paginaAtual: 1, 
            multiplicador: 1,
            configDataSource: Config,
            showModalImagem : false , 
            mensagemRetornoModalFormulario: {
                status: 0, 
                message: '' , 
            }, 
            modalFormulario: Object, 
            dump: null , 
        }
    },
    components: {
        Paginacao,
        ModalImagem,
        ModalFormulario, 
        ModalContainer,
        GridContainer ,  
    },
    methods: {
        childRetornaPagiancao(paginacaoRetorno , multiplicador) {
            this.paginaAtual = paginacaoRetorno;
            this.multiplicador = multiplicador;
        },
        
        childRetornaDataSourceFormulario( dataSource ) {
            this.dump = dataSource;
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
{{ dump }}
    <h1>Utils-ModalFormulario</h1>
        <ModalFormulario
            @enviarModalFormulario="childRetornaDataSourceFormulario"
            :mensagemRetornoPai="mensagemRetornoModalFormulario"
            >
        </ModalFormulario>
<br><br>
        <ModalContainer></ModalContainer>

<br> 
        <GridContainer></GridContainer>
</template>

