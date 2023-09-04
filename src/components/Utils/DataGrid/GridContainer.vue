<script lang="ts">
import GridOpcoes from "@/components/Utils/DataGrid/GridOpcoes.vue";
import DataGrid from "@/components/Utils/DataGrid/DataGrid.vue";
import DataGridDataSource from "@/assets/json/gridContainerDataSource.json";

export default {

    components: { 
        DataGrid, 
        GridOpcoes, 
    }, 
    data() {
        return {
            dataGridDataSource: DataGridDataSource,
            selectedRow : null ,         
        }
    }, 
    methods: { 
        childGridSelected(dataSource) {
            this.selectedRow = dataSource; 
        }, 
        childOpcaoDeletar(dataSource) { 
            
        }, 
        childOpcaoAdicionar(dataSource) {
            
        },
        childOpcaoEditar(dataSource) {
            
        },
    }

}
</script>
<template>
    <div class="container">
        <div class="row">
            <GridOpcoes :selectedRow="selectedRow"
                @deletar="childOpcaoDeletar"
                @adicionar="childOpcaoAdicionar" 
                @editar="childOpcaoEditar"
            ></GridOpcoes>
        </div>

        <div class="row">
            <DataGrid 
                :dataSource="dataGridDataSource"
                @gridSelected="childGridSelected">
            </DataGrid>
        </div>
    </div>
{{ selectedRow }}
</template>
<style scoped></style>