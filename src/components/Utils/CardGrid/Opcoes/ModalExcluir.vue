<script lang="ts">
export default {
    props: {
        message: {
            type: String,
            required: true,
        },
        title: {
            type: String,
            required: true,
        },


    },
    data() {
        return {
            showModal: false,
        }
    },
    emits: ['confirmar'],

    methods: {
        confirmar() {
            this.$emit('confirmar');
            this.showModal = false;
        },

    }
}
</script>
<template>
    <button class="mdc-button mdc-button--excluir" @click="showModal = true">
        <div class="mdc-button__ripple"></div>
        <span :class="'material-icons'">
            delete
        </span>
    </button>

    <div :class="{ 'showModal': showModal, 'hide': !showModal }">
        <div class="containerModalFormulario">
            <div class="modalFormulario rounded">
                <div class="mdc-card__primary-action">
                    <div class="mdc-card__media mdc-card__media--square">
                        <div class="mdc-card__media-content">
                            <h5>{{ title }}</h5>
                        </div>
                    </div>
                    <p class="text-muted">{{ message }}</p>
                    <!-- ... additional primary action content ... -->
                    <div class="mdc-card__ripple"></div>
                </div>
                <br>
                <!-- Validações dos botões de Envio e cancelar -->
                <div class="row">
                    <div class="col-6">
                        <button @click="showModal = false" class="mdc-button mdc-button--cancelar">
                            <span class="mdc-button__ripple"></span>
                            <span class="mdc-button__label">Cancelar</span>
                        </button>
                    </div>
                    <div class="col-6">
                        <button @click="confirmar" class="mdc-button mdc-button--confirmar">
                            <span class="mdc-button__ripple"></span>
                            <span class="mdc-button__label">Confirmar</span>
                        </button>
                    </div>

                </div>
            </div>
        </div>

    </div>
</template>
<style scoped>
@import "@/assets/scss/Utils/CardGrid/Modal/modalExcluir.scss";
@import 'material-icons/iconfont/material-icons.css';
</style>
