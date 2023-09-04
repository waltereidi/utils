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
            showModal: false , 
        }
    }
}
</script>
<template>
    <button :disabled="disabled" class="btn btn-danger btn-sm" @click="showModal = true">Excluir</button>
     <div :class="{ 'showModal': showModal, 'hide': !showModal }">
            <div class="containerModalFormulario">
                <div class="modalFormulario rounded">
                    <!-- Validações dos botões de Envio e cancelar -->
                   <div class="row">
                        <div class="col">
                            <button @click="showModal = false" class="btn btn-primary">Cancelar</button>
                        </div>
                    </div>
                </div>
             </div>
        
        </div>
    </template>
    <style scoped>
    @import "@/assets/css/utils/modal";
    </style>
