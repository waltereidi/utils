<script lang="ts">
import Card from "@/components/Utils/CardGrid/Card.vue";


export default {
    components: {
        Card,
    }
}
</script>
<template>
    <div class="container">

        <Card></Card>


    </div>
</template>

<style scoped >
.container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 20px;
    padding: 20px;
}
</style>