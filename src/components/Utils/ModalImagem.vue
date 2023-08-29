<script lang="ts">
export default { 
    props: {
            srcImagem: String, 
            heightModal: String,
            widthModal: String, 
            medidaModal: String,
    },
    methods: {
        abrirModal() {
            
        }
    }
    }
</script>
<template>
 <img :src="srcImagem" :style="{ width: `${widthModal}`}" @click="abrirModal">


</template>
<style scoped>

</style>