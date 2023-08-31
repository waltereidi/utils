<script lang="ts">

export default {

    props: {
        resposta:{
            type: Number,
            required: false 
        }
    },
    data() {
            return { 
                dataSource: {
                    nome: String, 
                    descricao: String, 
                }, 
                showModal: false , 
            }
    }, 
    methods: {
        retornaDataSource() {
            this.$emit('retornaDataSource', this.dataSource );
        },
    },
    emits: ['retornaDataSource'],  

    watch: {
        resposta() {
            if (this.resposta.status === 200) {
                this.showModal = close;
            }
        }
    }      
    }
   
</script>
<template>
    <button @click="showModal=true">Abrir Modal Formulario</button>
    <div :class="{ 'showModal': showModal, 'hide': !showModal }"> 
        <form>
            <fieldset>  
                <label>
                <input type="text" v-model="dataSource.nome" >Nome</label>
                <textarea v-model="dataSource.descricao"></textarea>
                <button classs="btn-success" @click="retornaDataSource">Salvar</button> 
                <button class="btn-primary" @click="showModal = false">Cancelar</button>
                <div v-if="resposta.status >=300" class="alert alert-danger" role="alert">
                    {{ resposta.message }}
                </div>

            </fieldset>
        </form>
    </div>

</template>
<style scoped>
.hide {
    display: none;
}

.showModal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    /* Cor de fundo com transparência */
    z-index: 1000;
    /* Coloque um valor alto para sobrepor outros elementos */
    display: flex;
    justify-content: center;
    align-items: center;
}

#modalImg {
    margin: auto 0 auto 0;
}

#modalButton {
    margin-left: 100%;
}</style>