<script lang="ts">
import MensagemErro from "@/components/Utils/MensagemErro.vue"
import { useVuelidate } from "@vuelidate/core";
import { required } from "@vuelidate/validators";

export default {
    setup() {
    return { v$ : useVuelidate() }  
    },
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
        }, 
        mensagemRetornoPai: {
            type: Object
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
    validations() {
        return { 
            dataSource: {
                nome: { required }, 
                descricao: { required } ,
            }
        }   
    },
    emits: ['enviarModalFormulario'], 
    methods: {
      
        montarRetornoFormulario() :object {
            return {
                nome: this.dataSource.nome, 
                descricao: this.dataSource.descricao, 
            }
        },
        enviarModalFormulario():void {
                const dataSource = this.montarRetornoFormulario();
                this.$emit('enviarModalFormulario', dataSource );

        },
        cancelarFormulario(): void{
            this.dataSource.nome = '';
            this.dataSource.descricao = '';

            this.showModal = false ; 
        }
    },
    components: {
        MensagemErro , 
    }

  
}

</script>
<template>
    <button class="btn btn-primary" @click="showModal = true">Abrir Modal Formulario</button>
    <div :class="{ 'showModal': showModal, 'hide': !showModal }">
        <div class="containerModalFormulario">
            <div class="modalFormulario rounded">
                <div class="form-group">
                    <div class="row">
                    <!-- Input -->
                        <div class="form-group">
                            <label for="exampleFormControlInput1">Nome</label>
                            <input type="text" v-model="dataSource.nome"
                                :class="{'form-control is-valid': !v$.dataSource.nome.$invalid ,
                                'form-control is-invalid': v$.dataSource.nome.$invalid }" placeholder="nome">
                            <!-- Validação -->
                            <div v-if="v$.dataSource.nome.$invalid"  class="invalid-feedback">Campo obrigatório</div>
                            <div class="valid-feedback" v-else></div>
                        </div>
                    </div>


                    <div class="row">
                        <!-- Input -->
                        <div class="form-group">
                            <label for="exampleFormControlTextarea1">Descrição</label>
                            <textarea v-model="dataSource.descricao" 
                                :class="{'form-control is-valid' : !v$.dataSource.descricao.$invalid ,
                                'form-control is-invalid' : v$.dataSource.descricao.$invalid }" rows="3" 
                                placeholder="Descricao...">
                            </textarea>
                            <!-- Validação -->
                            <div v-if="v$.dataSource.descricao.$invalid"  class="invalid-feedback">Campo obrigatório</div>
                            <div class="valid-feedback" v-else></div>
                        </div>
                    </div>
                    <br>

                    <!-- Validações dos botões de Envio e cancelar -->
                    <div class="row">
                        <div class="col">
                            <button @click="enviarModalFormulario" class="btn btn-success"
                            :disabled="v$.dataSource.descricao.$invalid"
                            >Enviar</button>
                        </div>
                        <div class="col">
                            <button @click="cancelarFormulario()" class="btn btn-primary">Cancelar</button>
                        </div>
                    </div>
                    
                    <!-- Mensagens de erro -->
                    <div class="row">
                            <MensagemErro :mensagemErro="mensagemErro"></MensagemErro>
                    </div>
                </div>
            </div>
         </div>
         
    </div>
</template>
<style scoped>
    @import "@/assets/css/utils/modal";
</style>