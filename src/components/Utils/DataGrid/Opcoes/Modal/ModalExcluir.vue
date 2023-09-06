<script lang="ts">
export default {
    props: {
        disabled: {
            type: Boolean,
            required: false,
            default: false
        }
    },
    data() {
        return {
            showModal: false,
        }
    }
}
</script>
<template>
    <button class="mdc-button mdc-button--outlined mdc-button--excluir" @click="showModal = true">
        <span :class="'material-icons'">
            delete
        </span>
        <span class="mdc-button__label">Deletar</span>
    </button>
    <div :class="{ 'showModal': showModal, 'hide': !showModal }">
        <div class="containerModalFormulario">
            <div class="modalFormulario rounded">
                <!-- Validações dos botões de Envio e cancelar -->
                <div class="row">
                    <div class="col">
                        <button @click="showModal = false"
                            class="mdc-button mdc-button--outlined mdc-button--cancelar">Cancelar</button>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>
<style scoped>
@import "@/assets/css/utils/modal";
@import "@/assets/scss/Utils/DataGrid/modal.scss";
@import 'material-icons/iconfont/material-icons.css';
</style>
