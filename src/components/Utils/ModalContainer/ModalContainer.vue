<script lang="ts">
export default {
    data() {
        return {
            showModal: false , 
        }
    }
}
</script>
<template>
    <button class="btn btn-primary" @click="showModal = true">Abrir Modal Cotainer</button>
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
