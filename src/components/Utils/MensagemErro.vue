<script lang="ts">
export default {
    props: {
        mensagemErro: {
            type: Array, 
            required:true ,
        },
    }
}

</script>
<template>
    <div class="formularioErros" v-for="erro in mensagemErro">
        <div :class="{ 'alert alert-danger': (erro.code == 'danger'), 
                       'alert alert-warning': (erro.code == 'warning'), 
                       'alert alert-success': (erro.code == 'success'),
                       'alert alert-primary': (erro.code == 'primary')
                       }" role="alert">
            {{ erro.message }}
        </div>
    </div>

</template>
<style scoped>
</style>