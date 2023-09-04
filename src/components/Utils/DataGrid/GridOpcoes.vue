<script lang="ts">
import ModalExcluir from "@/components/Utils/DataGrid/Opcoes/Modal/ModalExcluir.vue";
import ModalFormularioEditar from "@/components/Utils/DataGrid/Opcoes/Modal/ModalFormularioEditar.vue";
import ModalFormularioAdicionar from "@/components/Utils/DataGrid/Opcoes/Modal/ModalFormularioAdicionar.vue";

export default {
    props: {
        selectedRow: {
            type: Object!,
            required: true,
        },
        
    },
    components: {
        ModalExcluir,
        ModalFormularioEditar,
        ModalFormularioAdicionar,
    }
}
</script>
<template>
    <div class="row justify-content-md-right">
        <div class="col-9"></div>
        <div class="col-1">
            <ModalExcluir
                :disabled="selectedRow===null"
                :dataSource="selectedRow">
            </ModalExcluir>
        </div>
        <div class="col-1">
            <ModalFormularioEditar 
                :disabled="selectedRow===null"
                :dataSource="selectedRow">
            </ModalFormularioEditar>
        </div>
        <div class="col-1">
            <ModalFormularioAdicionar></ModalFormularioAdicionar>
        </div>
    </div>

</template>
<style scoped>

</style>