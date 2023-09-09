<script lang="ts">
import config from "@/assets/json/bibliotecaconfig.json";
import ModalFormulario from './Opcoes/ModalFormulario.vue';
import ModalExcluir from './Opcoes/ModalExcluir.vue';
export default {
    props:
    {
        dataSource: {
            type: Object,
            required: true,

        }
    },
    components: {
        ModalFormulario,
        ModalExcluir,
    },
    data() {
        return {
            configDataSource: config,
        }
    },
    methods: {
        childEnviarModalFormulario() {

        }
    }
}
</script>
<template>
    <div class="mdc-card mdc-card--outlined">
        <div class="mdc-card__primary-action">
            <div class="mdc-card__media mdc-card__media--square mdc-card">
                <div class="mdc-card__media-content">
                    <h4>{{ dataSource.titulo }}</h4>
                    <h5><sub>
                            <p class="text-muted">{{ dataSource.autores_nome }}</p>
                        </sub></h5>
                    <div class="cardImage">
                        <img :src="dataSource.capalivro ?? configDataSource.capaLivroDefault" />
                    </div>
                </div>
            </div>
            <div class="mdc-card__ripple"></div>
        </div>
        <div class="mdc-card__actions">
            <div class="mdc-card__action-buttons">
                <div class="alignleft">
                    <ModalFormulario :parentDataSource="dataSource"
                        @enviarModalFormularioAdicionar="childEnviarModalFormulario"></ModalFormulario>
                </div>
                <div class="alignright">
                    <ModalExcluir :title="'Confirma exclusão'"
                        :message="'Após confirmar a exclusão do livro sua ação não podera ser desfeita.'"></ModalExcluir>
                </div>
            </div>

        </div>
    </div>
</template>

<style scoped>
@import "@/assets/scss/Utils/CardGrid/cardGrid.scss";
@import "material-icons/iconfont/material-icons.css";
</style>