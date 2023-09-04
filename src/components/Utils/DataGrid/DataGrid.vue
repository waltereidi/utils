<script lang="ts">
export default { 
    props: { 
        dataSource: {
            type: Object!, 
            required: true, 
        }
    },
    data(){
        return { 
            selectedRow: null, 
        }
    },
    methods: { 
        selectRow(row, index) {
            this.selectedRow = index;         
            this.$emit('gridSelected', row);
        }
    }, 
    emits: ['gridSelected'], 
    
}
</script>
<template>
    <table class="table table-bordered"> 
        <thead class="thead-dark"> 
            <th> CapaLivro </th>
            <th> ISBN </th> 
            <th> Titulo </th>
        </thead>
            <tr v-for="(row , index ) in dataSource" :key="index" @click="selectRow(row , index)" :class="{'bg-primary': (index === selectedRow)}">
                <td> {{row.capalivro }} </td>
                <td> {{row.isbn }} </td> 
                <td> {{row.titulo }} </td>
            </tr>

    </table>

</template>
<style scoped> 

</style>