<script lang="ts">

export default {
  
    }
   
</script>
<template>
    <h1></h1>
</template>
<style scoped>
.hide {
    display: none;
}

.showModal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    /* Cor de fundo com transparência */
    z-index: 1000;
    /* Coloque um valor alto para sobrepor outros elementos */
    display: flex;
    justify-content: center;
    align-items: center;
}

#modalImg {
    margin: auto 0 auto 0;
}

#modalButton {
    margin-left: 100%;
}</style>