<script lang="ts">
import MensagemErro from "@/components/Utils/MensagemErro.vue"

export default {
    props: { 
        dataSource: {
          type: Object ,
          requied: true, 
        },
        mensagemRetornoPai: {
            type: Object
        },
        disabled: {
            type: Boolean,
            required: false,
            default: false
        }
    },
    data(){ 
        return {
            showModal: false, 
            mensagemErro: [],
            dataSource: {
                nome: this.nome, 
                nomeMensagem:'Este campo deve ser preenchido',
                descricao: this.descricao,
                descricaoMensagem : 'Este campo deve ser preenchido.',
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
    <button :disabled="disabled" class="btn btn-primary btn-sm" @click="showModal = true">Adicionar</button>
    <div :class="{ 'showModal': showModal, 'hide': !showModal }">
        <div class="containerModalFormulario">
            <div class="modalFormulario rounded">
                <div class="form-group">
                    <div class="row">
                    <!-- Input -->
                        <div class="form-group">
                            <label for="exampleFormControlInput1">Nome</label>
                            <input type="text" v-model="dataSource.nome"
                                :class="{'form-control is-valid': (dataSource.nome.length > 0),
                                'form-control is-invalid': (dataSource.nome.length === 0) }" placeholder="nome">
                            <!-- Validação -->
                            <div v-if="dataSource.nome.length == 0"  class="invalid-feedback">{{ dataSource.nomeMensagem }}</div>
                            <div class="valid-feedback" v-else></div>
                        </div>
                    </div>


                    <div class="row">
                        <!-- Input -->
                        <div class="form-group">
                            <label for="exampleFormControlTextarea1">Descrição</label>
                            <textarea v-model="dataSource.descricao" 
                                :class="{'form-control is-valid' :(dataSource.descricao.length > 0) ,
                                'form-control is-invalid' : (dataSource.descricao.length === 0) }" rows="3" 
                                placeholder="Descricao...">
                            </textarea>
                            <!-- Validação -->
                            <div v-if="dataSource.descricao.length==0"  class="invalid-feedback">{{dataSource.descricaoMensagem }}</div>
                            <div class="valid-feedback" v-else></div>
                        </div>
                    </div>
                    <br>

                    <!-- Validações dos botões de Envio e cancelar -->
                    <div class="row">
                        <div class="col">
                            <button @click="enviarModalFormulario" class="btn btn-success"
                            :disabled="(dataSource.nome.length === 0) ||
                                       (dataSource.nome.length === 0)"
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