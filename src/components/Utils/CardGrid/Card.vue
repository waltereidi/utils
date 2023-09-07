<script lang="ts">

import ModalFormulario from './Opcoes/ModalFormulario.vue';

export default {
    components: {
        ModalFormulario,

    }
}
</script>
<template>
    <div class="mdc-card mdc-card--outlined">
        <div class="mdc-card__primary-action">
            <div class="mdc-card__media mdc-card__media--square mdc-card">
                <div class="mdc-card__media-content">
                    <h4>Titulo</h4>
                    <h5><sub>Sub</sub></h5>
                </div>
            </div>
            <!-- ... additional primary action content ... -->
            <div class="mdc-card__ripple"></div>
        </div>
        <div class="mdc-card__actions">
            <div class="mdc-card__action-buttons">
                <ModalFormulario></ModalFormulario>
                <button class="mdc-button mdc-card__action mdc-card__action--button">
                    <div class="mdc-button__ripple"></div>
                    <span class="mdc-button__label">Action 2</span>
                </button>
            </div>

        </div>
    </div>
</template>

<style scoped>
@import "@/assets/scss/Utils/CardGrid/cardGrid.scss";
@import "material-icons/iconfont/material-icons.css";
</style>