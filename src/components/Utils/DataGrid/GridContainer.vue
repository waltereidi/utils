<script lang="ts">
import GridOpcoes from "@/components/Utils/DataGrid/GridOpcoes.vue";
import DataGrid from "@/components/Utils/DataGrid/DataGrid.vue";

export default {
    components: { 
        DataGrid, 
        GridOpcoes, 

    }
}
</script>
<template>
    <div class="container">
        <div class="row">
            <GridOpcoes></GridOpcoes>
        </div>

        <div class="row">
            <DataGrid></DataGrid>
        </div>
    </div>

</template>
<style scoped></style>