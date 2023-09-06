<script lang="ts">
import MensagemErro from '@/components/Utils/MensagemErro.vue'
import { useVuelidate } from '@vuelidate/core'
import { required, url, minLength } from '@vuelidate/validators'
import { MdButton, MdContent, MdTabs } from 'vue-material/dist/components'



export default {
    setup() {
        return { v$: useVuelidate() }
    },
    props: {
        selectedRow: {
            type: Object,
            required: false,
        },
        nomeBotao: {
            type: String,
            required: true,
        },
        disabled: {
            type: Boolean,
            required: true,
        },
    },
    data() {
        return {
            showModal: false,
            mensagemErro: [],
            dataSource: {
                id: this.id,
                titulo: this.titulo,
                descricao: this.descricao,
                isbn: this.isbn,
                capalivro: this.capalivro,
                editoras_nome: this.editoras_nome,
                autores_nome: this.autores_nome,
                idioma: this.idioma,
                genero: this.genero
            }
        }
    },
    validations() {
        return {
            dataSource: {
                titulo: { required, minLength: minLength(4) },
                capalivro: { url },
                editoras_nome: { required, minLength: minLength(4) },
                autores_nome: { required, minLength: minLength(4) },
            }
        }
    },
    emits: ['enviarModalFormularioAdicionar'],
    methods: {

        enviarModalFormulario(): void {
            this.$emit('enviarModalFormularioAdicionar', this.dataSource)
        },
        cancelarFormulario(): void {
            this.dataSource = {
                id: '',
                titulo: '',
                descricao: '',
                isbn: '',
                capalivro: '',
                editoras_nome: '',
                autores_nome: '',
                idioma: '',
                genero: ''
            };
            this.showModal = false;
        }
    },
    components: {
        MensagemErro
    },

}
</script>
<template>
    <button
        :class="{ 'mdc-button mdc-button--outlined mdc-button--adicionar': (nomeBotao == 'Adicionar'), 'mdc-button mdc-button--outlined mdc-button--editar': (nomeBotao == 'Editar') }"
        @click="showModal = true">
        <span :class="'material-icons'">
            {{ (nomeBotao === 'Adicionar') ? 'add' : 'edit' }}
        </span>
        <span class="mdc-button__label">{{ nomeBotao }}</span>
    </button>
    <div :class="{ showModal: showModal, hide: !showModal }">

        <div class="col-3"></div>
        <div class="col-6">

            <div class="containerModalFormulario">
                <div class="modalFormulario rounded">
                    <div class="row">
                        <div class="col-4">
                            <div class="row">
                                <img v-if="!v$.dataSource.capalivro.$invalid" class="rounded mx-auto d-block"
                                    :src="dataSource.capalivro" />
                            </div>
                        </div>
                        <div class="col-8">
                            <div class="row">
                                <div class="form-group">
                                    <!-- Input -->
                                    <div class="form-group">
                                        <label for="exampleFormControlInput1">Título</label>
                                        <input type="text" v-model="dataSource.titulo" :class="{
                                            'form-control is-valid': !v$.dataSource.titulo.$invalid,
                                            'form-control is-invalid': v$.dataSource.titulo.$invalid
                                        }" placeholder="Título do livro" />
                                        <!-- Validação -->
                                        <div v-if="v$.dataSource.titulo.$invalid" class="invalid-feedback">
                                            O nome deve estar preenchido
                                        </div>
                                        <div class="valid-feedback" v-else></div>
                                    </div>
                                </div>
                                <div class="col-6">
                                    <div class="row">
                                        <!-- Input -->
                                        <div class="form-group">
                                            <label for="exampleFormControlInput1">ISBN</label>
                                            <input type="text" v-model="dataSource.isbn" class="form-control"
                                                placeholder="ISBN do livro" />
                                        </div>
                                    </div>
                                </div>
                                <div class="row">
                                    <div class="col-6">
                                        <div class="form-group">
                                            <label for="exampleFormControlInput1">Nome do autor</label>
                                            <input type="text" v-model="dataSource.autores_nome" :class="{
                                                'form-control is-valid': !v$.dataSource.autores_nome.$invalid,
                                                'form-control is-invalid': v$.dataSource.autores_nome.$invalid
                                            }" placeholder="Nome do autor" />
                                            <div v-if="v$.dataSource.autores_nome.$invalid" class="invalid-feedback">
                                                Preencha o nome do autor
                                            </div>
                                            <div class="valid-feedback" v-else></div>
                                        </div>
                                    </div>
                                    <div class="col-6">
                                        <div class="form-group">
                                            <label for="exampleFormControlInput1">Nome da editora</label>
                                            <input type="text" v-model="dataSource.editoras_nome" :class="{
                                                'form-control is-valid': !v$.dataSource.editoras_nome.$invalid,
                                                'form-control is-invalid': v$.dataSource.editoras_nome.$invalid
                                            }" placeholder="Nome da editora" />
                                            <div v-if="v$.dataSource.editoras_nome.$invalid" class="invalid-feedback">
                                                Preencha o nome da editora
                                            </div>
                                            <div class="valid-feedback" v-else></div>
                                        </div>
                                    </div>
                                </div>
                                <div class="row">
                                    <!-- Input -->
                                    <div class="form-group">
                                        <label for="exampleFormControlInput1">Capa do livro</label>
                                        <input type="url" v-model="dataSource.capalivro" :class="{
                                            'form-control': !v$.dataSource.capalivro.$invalid,
                                            'form-control is-invalid': v$.dataSource.capalivro.$invalid
                                        }" placeholder="url" />
                                        <!-- Validação -->
                                        <div v-if="v$.dataSource.capalivro.$invalid" class="invalid-feedback">
                                            url inválida
                                        </div>
                                        <div class="valid-feedback" v-else></div>
                                    </div>
                                </div>

                                <div class="row">
                                    <div class="col-6">
                                        <!-- Input -->
                                        <div class="form-group">
                                            <label for="exampleFormControlInput1">Gênero</label>
                                            <input type="text" v-model="dataSource.genero" class="form-control"
                                                placeholder="Gênero do livro" />
                                            <!-- Validação -->
                                        </div>
                                    </div>


                                    <div class="col-6">
                                        <!-- Input -->
                                        <div class="form-group">
                                            <label for="exampleFormControlInput1">Idioma</label>
                                            <input type="text" v-model="dataSource.idioma" class="form-control"
                                                placeholder="Idioma do livro" />
                                            <!-- Validação -->
                                        </div>
                                    </div>
                                </div>
                                <div class="row">
                                    <!-- Input -->
                                    <div class="form-group">
                                        <label>Descrição:</label>
                                        <textarea v-model="dataSource.descricao" class="form-control" rows="3"
                                            placeholder="Descricao..."></textarea>
                                        <br>
                                        <!-- Validação -->

                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Validações dos botões de Envio e cancelar -->
                        <div class="row">

                            <div class="col-1">
                                <button @click="cancelarFormulario()"
                                    class="mdc-button mdc-button--raised mdc-button--cancelar">Cancelar</button>
                            </div>
                            <div class="col-10"></div>
                            <div class="col-1">
                                <button @click="enviarModalFormulario"
                                    class="mdc-button mdc-button--raised mdc-button--confirmar"
                                    :disabled="v$.dataSource.$invalid">
                                    Enviar
                                </button>
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
        <div class="col-3"></div>
    </div>
</template>
<style scoped>
@import '@/assets/css/utils/modal';
@import "@/assets/scss/Utils/DataGrid/modal.scss";
@import 'material-icons/iconfont/material-icons.css';
</style>
