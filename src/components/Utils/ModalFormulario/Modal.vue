<script lang="ts">
import { stringify } from 'querystring';


export default {
    props: { 
        nome: {
            type: String,
            required: false,
            default:"",
        }, 
        descricao: {
            type: String, 
            required: false, 
            default:"",
        }
    },
    data(){ 
        return {
            showModal: false, 
            mensagemErro: [],
            dataSource: {
                nome: this.nome, 
                descricao: this.descricao,
            }
        }
    },
    emits: ['enviarModalFormulario'], 
    methods: {
        validarEnvio():array {
            this.mensagemErro = [];
            (this.dataSource.nome.length) ? null : this.mensagemErro.push({ code: "danger", message: "O campo nome não pode estar vazio." })  ; 
            (this.dataSource.descricao.length) ? null : this.mensagemErro.push({ code: "warning" , message:"O campo descricao não pode estar vazio."}); 
            return this.mensagemErro;
        },
        montarRetornoFormulario() :object {
            return {
                nome: this.nome, 
                descricao: this.descricao, 
            }
        },
        enviarModalFormulario():void {
            if (this.validarEnvio().length) {
                this.$emit('enviarModalFormulario', dataSource);
            } 
            
        }
    },

  
}

</script>
<template>
    <button @click="showModal = true">Abrir Modal Formulario</button>
    <div :class="{ 'showModal': showModal, 'hide': !showModal }">
        <div class="modalFormulario">
            <div class="container-sm">
                <div class="form-group">
                    <div class="row">
                        <div class="form-group">
                                <label for="exampleFormControlInput1">Nome</label>
                                <input type="text" v-model="dataSource.nome" class="form-control" placeholder="nome">
                        </div>
                    </div>
                    <div class="row">
                        <div class="form-group">
                            <label for="exampleFormControlTextarea1">Descrição</label>
                            <textarea v-model="dataSource.descricao" class="form-control" rows="3" ></textarea>
                        </div>
                    </div>
                    <div class="row">
                        <div class="col">
                            <button @click="enviarModalFormulario" class="btn btn-success"> Enviar</button>
                        </div>
                        <div class="col">
                            <button @click="showModal = false" class="btn btn-primary">Cancelar</button>
                        </div>
                    </div>
                    <div class="row">
                        <div class="formularioErros" v-for="erro in mensagemErro">
                            <div :class="{ 'alert alert-danger': (erro.code == 'danger'), 'alert alert-warning': (erro.code == 'warning') }" role="alert">
                                {{ erro.message }}
                            </div>
                        </div>
                    </div>
                </div>
            </div>
         </div>
         
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
    overflow: hidden;
}

#modalImg {
    margin: auto 0 auto 0;
}

#modalButton {
    margin-left: 100%;
}
.modalFormulario{
    height: 50vh;
    width: 60vh;
    background-color: white;
}
</style>