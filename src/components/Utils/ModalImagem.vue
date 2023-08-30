<script lang="ts">
export default { 
    props: {
            srcImagem: String, 
            showModal: Boolean ,
    },
    data() {
        return {
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
                this.fecharModal(); 
            }
        }, 
        fecharModal() {
            this.$emit( "fecharModal");
        }
    },
    emits: ['fecharModal'],
      
    }
</script>
<template>

    <div :class="{ 'showModal': showModal, 'hide': !showModal }"> 
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
    }
    #modalImg{
        margin :auto 0 auto 0;
    }
    #modalButton {
        margin-left:100%;
    }
    

</style>