<script lang="ts">
export default { 
    props: {
            srcImagem: String, 
    },
    data() {
        return {
            showModal : false
        }
    },
    
    watch: {
        showModal() {
            if (this.showModal ) {
                window.addEventListener('keydown', this.keyListener);
            }
        }
    }, 
    methods: {
        keyListener(event) {
            if (event.keyCode === 27) {
                this.showModal = false; 
            }
        }, 
        fecharModal() {
            this.showModal = false; 
        }
    },
    emits: ['fecharModal'],
      
    }
</script>
<template>
    <img  class="img-thumbnail" :src="srcImagem" @click="showModal = true" style="height: 50px;">
    <div :class="{ 'showModal': showModal, 'hide': !showModal }" @click="showModal=false"> 
        <div class="row">
                <button id="modalButton" type="button" class="btn-close btn-close-white" aria-label="Close" @click="fecharModal"></button>
                <img :src="srcImagem" id="modalImg"  >

        </div>
    </div>

</template>
<style scoped>
    .hide{
        display:none ;
    }
    .showModal{
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.5); /* Cor de fundo com transparência */
        z-index: 1000; /* Coloque um valor alto para sobrepor outros elementos */
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;
    }
    #modalImg{
        margin :auto 0 auto 0;
    }
    #modalButton {
        margin-left:100%;
    }
    

</style>