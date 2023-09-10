<script lang="ts">
import Card from "@/components/Utils/CardGrid/Card.vue";
import LivrosDataSource from "@/assets/json/gridContainerDataSource.json";
import ModalFormularioAdicionar from "./Opcoes/ModalFormularioAdicionar.vue";
import Paginacao from "../Paginacao.vue";

export default {
    components: {
        Card,
        ModalFormularioAdicionar,
        Paginacao,
    },
    data() {
        return {
            livrosDataSource: LivrosDataSource,
            searchBar: '',
        }
    },
    methods: {
        buscar() {

        },
        childRetornaPaginacao(paginacao, multiplicador) {


        }
    }

}
</script>
<template>
    <div class="container">

        <div class="border cardGridHeader">

            <div class="leftSearch">
                <label class="mdc-text-field mdc-text-field--filled mdc-text-field--with-trailing-icon">
                    <span class="mdc-floating-label" id="my-label-id" v-if="searchBar === ''">Procurar</span>
                    <input v-model="searchBar" class="mdc-text-field__input" type="text" aria-labelledby="my-label-id">
                    <i @click="buscar" class="material-icons mdc-text-field__icon mdc-text-field__icon--trailing"
                        tabindex="0" role="button">search</i>
                </label>
            </div>
            <div class="rightButton">
                <ModalFormularioAdicionar></ModalFormularioAdicionar>
            </div>

        </div>
        <div class="cardGrid container">
            <div v-for="livro in livrosDataSource">
                <Card :dataSource="livro"></Card>
            </div>
        </div>
        <div class="cardGridFooter">

            <Paginacao :quantidade="30" :multiplicador="6" :limitePaginacao="10" :travarPaginacao="false"
                @retornaPaginacao="childRetornaPaginacao"></Paginacao>
        </div>
    </div>
</template>

<style scoped >
@import 'material-icons/iconfont/material-icons.css';
@import '@/assets/scss/Utils/CardGrid/cardGridContainer.scss';
</style>