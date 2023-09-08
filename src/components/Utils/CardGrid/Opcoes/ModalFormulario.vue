<script lang="ts">
import config from "@/assets/json/bibliotecaconfig.json";
import MensagemErro from '@/components/Utils/MensagemErro.vue'
import { useVuelidate } from '@vuelidate/core'
import { required, url, minLength } from '@vuelidate/validators'
import { MdButton, MdContent, MdTabs } from 'vue-material/dist/components'



export default {
    setup() {
        return { v$: useVuelidate() }
    },
    props: {
        parentDataSource: {
            type: Object,
            required: true,
        },

    },
    data() {
        return {
            configDataSource: config,
            showModal: false,
            mensagemErro: [],
            dataSource: {
                id: this.parentDataSource == null ? '' : this.parentDataSource.id,
                titulo: this.parentDataSource == null ? '' : this.parentDataSource.titulo,
                descricao: this.parentDataSource == null ? '' : this.parentDataSource.descricao,
                isbn: this.parentDataSource == null ? '' : this.parentDataSource.isbn,
                capalivro: this.parentDataSource == null ? '' : this.parentDataSource.capalivro,
                editoras_nome: this.parentDataSource == null ? '' : this.parentDataSource.editoras_nome,
                autores_nome: this.parentDataSource == null ? '' : this.parentDataSource.autores_nome,
                idioma: this.parentDataSource == null ? '' : this.parentDataSource.idioma,
                genero: this.parentDataSource == null ? '' : this.parentDataSource.genero,
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
    <button class="mdc-button mdc-card__action mdc-card__action--button" @click="showModal = true">
        <div class="mdc-button__ripple"></div>
        <span :class="'material-icons'">
            edit
        </span>
    </button>
    <div :class="{ 'showModal': showModal, 'hide': !showModal }">
        <div class="containerModalFormulario">
            <div class="mdc-card mdc-card--outlined">
                <div class="row">
                    <div class="col-6">
                        <div class="row">

                            <img class="rounded mx-auto d-block"
                                :src="!v$.dataSource.capalivro.$invalid ? configDataSource.capaLivroDefault : dataSource.capalivro" />

                        </div>
                    </div>
                    <div class="col-6">
                        <div class="row">
                            <!-- Input -->
                            <label class="mdc-text-field mdc-text-field--filled mdc-text-field--label-floating">
                                <span class="mdc-text-field__ripple"></span>
                                <span class="mdc-floating-label mdc-floating-label--float-above">
                                    <span
                                        :class="{ 'errorLabel': v$.dataSource.titulo.$invalid, '': !v$.dataSource.titulo.$invalid }">Titulo</span>
                                </span>
                                <input v-model="dataSource.titulo" class="mdc-text-field__input" type="text"
                                    aria-labelledby="my-label-id" maxlength="60">
                                <span class="mdc-line-ripple"></span>
                                <div class="mdc-text-field-helper-line">
                                    <div class="mdc-text-field-character-counter">{{ dataSource.titulo.length }} /
                                        60
                                    </div>
                                </div>
                            </label>
                            <div class="col-6">
                                <div class="row">
                                    <!-- Input -->
                                    <label class="mdc-text-field mdc-text-field--filled mdc-text-field--label-floating">
                                        <span class="mdc-text-field__ripple"></span>
                                        <span class="mdc-floating-label mdc-floating-label--float-above">
                                            ISBN
                                        </span>
                                        <input v-model="dataSource.isbn" class="mdc-text-field__input" type="text"
                                            aria-labelledby="my-label-id" maxlength="20">
                                        <span class="mdc-line-ripple"></span>
                                        <div class="mdc-text-field-helper-line">
                                            <div class="mdc-text-field-character-counter">{{ dataSource.isbn.length }} /
                                                20
                                            </div>
                                        </div>
                                    </label>
                                </div>
                            </div>
                            <div class="row">
                                <div class="col-6">
                                    <label class="mdc-text-field mdc-text-field--filled mdc-text-field--label-floating">
                                        <span class="mdc-text-field__ripple"></span>
                                        <span class="mdc-floating-label mdc-floating-label--float-above">
                                            <span
                                                :class="{ 'errorLabel': v$.dataSource.autores_nome.$invalid, '': !v$.dataSource.autores_nome.$invalid }">Nome
                                                do autor</span>
                                        </span>
                                        <input v-model="dataSource.autores_nome" class="mdc-text-field__input" type="text"
                                            aria-labelledby="my-label-id" maxlength="60">
                                        <span class="mdc-line-ripple"></span>
                                        <div class="mdc-text-field-helper-line">
                                            <div class="mdc-text-field-character-counter">{{ dataSource.autores_nome.length
                                            }} /
                                                60
                                            </div>
                                        </div>
                                    </label>
                                </div>
                                <div class="col-6">
                                    <label class="mdc-text-field mdc-text-field--filled mdc-text-field--label-floating">
                                        <span class="mdc-text-field__ripple"></span>
                                        <span class="mdc-floating-label mdc-floating-label--float-above">
                                            <span
                                                :class="{ 'errorLabel': v$.dataSource.editoras_nome.$invalid, '': !v$.dataSource.editoras_nome.$invalid }">Nome
                                                da editora</span>
                                        </span>
                                        <input v-model="dataSource.editoras_nome" class="mdc-text-field__input" type="text"
                                            aria-labelledby="my-label-id" maxlength="60">
                                        <span class="mdc-line-ripple"></span>
                                        <div class="mdc-text-field-helper-line">
                                            <div class="mdc-text-field-character-counter">{{ dataSource.editoras_nome.length
                                            }} /
                                                60
                                            </div>
                                        </div>
                                    </label>
                                </div>
                            </div>
                            <div class="row">
                                <br>
                                <!-- Input -->
                                <label class="mdc-text-field mdc-text-field--filled mdc-text-field--label-floating">
                                    <span class="mdc-text-field__ripple"></span>
                                    <span class="mdc-floating-label mdc-floating-label--float-above">
                                        <span
                                            :class="{ 'errorLabel': v$.dataSource.capalivro.$invalid, '': !v$.dataSource.capalivro.$invalid }">Url
                                            da imagem da capa do livro</span>
                                    </span>
                                    <input v-model="dataSource.capalivro" class="mdc-text-field__input" type="text"
                                        aria-labelledby="my-label-id" maxlength="2048">
                                    <span class="mdc-line-ripple"></span>
                                    <div class="mdc-text-field-helper-line">
                                        <div class="mdc-text-field-character-counter"><span
                                                v-if="v$.dataSource.capalivro.$invalid" class="errorLabel">Url
                                                inválida</span>
                                        </div>
                                    </div>
                                </label>
                            </div>

                            <div class="row">
                                <div class="col-6">
                                    <!-- Input -->
                                    <label class="mdc-text-field mdc-text-field--filled mdc-text-field--label-floating">
                                        <span class="mdc-text-field__ripple"></span>
                                        <span class="mdc-floating-label mdc-floating-label--float-above">
                                            Gênero do livro
                                        </span>
                                        <input v-model="dataSource.genero" class="mdc-text-field__input" type="text"
                                            aria-labelledby="my-label-id" maxlength="30">
                                        <span class="mdc-line-ripple"></span>
                                        <div class="mdc-text-field-helper-line">
                                            <div class="mdc-text-field-character-counter">
                                                {{ dataSource.genero.length }} / 30
                                            </div>
                                        </div>
                                    </label>
                                </div>


                                <div class="col-6">
                                    <!-- Input -->
                                    <label class="mdc-text-field mdc-text-field--filled mdc-text-field--label-floating">
                                        <span class="mdc-text-field__ripple"></span>
                                        <span class="mdc-floating-label mdc-floating-label--float-above">
                                            Idioma do livro
                                        </span>
                                        <input v-model="dataSource.idioma" class="mdc-text-field__input" type="text"
                                            aria-labelledby="my-label-id" maxlength="30">
                                        <span class="mdc-line-ripple"></span>
                                        <div class="mdc-text-field-helper-line">
                                            <div class="mdc-text-field-character-counter">
                                                {{ dataSource.idioma.length }} / 30
                                            </div>
                                        </div>
                                    </label>
                                </div>
                            </div>
                            <br>
                            <div class="row">
                                <!-- Input -->
                                <div class="spacing">
                                    <p></p>
                                </div>
                                <label
                                    class="mdc-text-field mdc-text-field--outlined mdc-text-field--textarea mdc-text-field--with-internal-counter">
                                    <span class="mdc-notched-outline">
                                        <span class="mdc-notched-outline__leading"></span>
                                        <span class="mdc-notched-outline__notch">
                                            <span v-if="dataSource.descricao.length == 0"
                                                class="mdc-floating-label mdc-floating-label--float-above"><br>Descrição
                                                do livro</span>
                                        </span>
                                        <span class="mdc-notched-outline__trailing"></span>
                                    </span>

                                    <span class="mdc-text-field__resizer">
                                        <textarea v-model="dataSource.descricao" class="mdc-text-field__input"
                                            aria-labelledby="my-label-id" rows="5" cols="222" maxlength="2048"></textarea>
                                        <span class="mdc-text-field-character-counter">{{ dataSource.descricao.length }} /
                                            2048</span>
                                    </span>
                                </label>
                            </div>
                        </div>
                    </div>

                    <!-- Validações dos botões de Envio e cancelar -->
                    <div class="row">

                        <div class="col-1">
                            <button @click="cancelarFormulario()"
                                class="mdc-button mdc-button--raised mdc-button--cancelar">Cancelar
                            </button>
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
</template>
<style scoped>
@import "@/assets/scss/Utils/CardGrid/Modal/modalFormulario.scss";
@import 'material-icons/iconfont/material-icons.css';
</style>