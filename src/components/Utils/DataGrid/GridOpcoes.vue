<script lang="ts">
import ModalExcluir from "@/components/Utils/DataGrid/Opcoes/Modal/ModalExcluir.vue";
import ModalFormulario from "@/components/Utils/DataGrid/Opcoes/Modal/ModalFormulario.vue";

export default {
    props: {
        selectedRow: {
            type: Object!,
            required: true,
        },
    },
    components: {
        ModalExcluir,
        ModalFormulario,
    }
}
</script>
<template>
    <div class="row justify-content-md-right">
        <div class="col-6"></div>
        <div class="col-6">
            <ModalExcluir :disabled="selectedRow === null" :dataSource="selectedRow">
            </ModalExcluir>
            <ModalFormulario :nomeBotao="'Editar'" :disabled="selectedRow === null" :selectedRow="selectedRow">
            </ModalFormulario>
            <ModalFormulario :nomeBotao="'Adicionar'" :disabled="false"></ModalFormulario>
        </div>
    </div>
</template>
<style scoped></style>