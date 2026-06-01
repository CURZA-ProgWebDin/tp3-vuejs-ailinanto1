<template>
    <div class="contenedor-paneles">
        <div class="seccion-normal">
            <button @click="tabActivo = 'todos'">Todos</button>
            <button @click="tabActivo = 'electronica'">Electronica</button>
            <button @click="tabActivo = 'perifericos'">Periféricos</button>
        
            <tabTodos v-if="tabActivo === 'todos'" />
            <tabElectronica v-else-if="tabActivo === 'electronica'" />
            <tabPerifericos v-else-if="tabActivo === 'perifericos'" />
        </div>
        <div class="seccion-keepAlive">
            <button @click="tabActivoConKeepAlive = 'todos'">Todos</button>
            <button @click="tabActivoConKeepAlive = 'electronica'">Electronica</button>
            <button @click="tabActivoConKeepAlive = 'perifericos'">Periféricos</button>
            <KeepAlive>
                <tabTodos v-if="tabActivoConKeepAlive === 'todos'" />
                <tabElectronica v-else-if="tabActivoConKeepAlive === 'electronica'" />
                <tabPerifericos v-else-if="tabActivoConKeepAlive === 'perifericos'" />
            </KeepAlive>
        </div>
    </div>
    </template>
<script setup>
    import { ref } from 'vue';
    import tabTodos from './tabs/tabTodos.vue'
    import tabElectronica from './tabs/tabElectronica.vue'
    import tabPerifericos from './tabs/tabPerifericos.vue';

    const tabActivo = ref('todos')
    const tabActivoConKeepAlive = ref('todos')
</script>
<style scoped>
    .contenedor-paneles {
        display: table;
        width: 100%;
        table-layout: fixed;
        border-collapse: separate;
        border-spacing: 20px; 
        margin-top: 10px;
    }
    .seccion-normal, .seccion-keepAlive {
        display: table-cell;
        vertical-align: top;
        background-color: #656565; 
        border: 1px solid #454552;
        border-radius: 12px;
        padding: 20px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
    }
    button {
        background-color: #232329;
        color: #cccccc;
        border: 1px solid #3d3d47;
        padding: 10px 16px;
        margin-right: 8px;
        margin-bottom: 20px;
        border-radius: 6px;
        cursor: pointer;
        font-weight: bold;
        font-size: 0.9rem;
        transition: all 0.25s ease-in-out;
    }
    button:hover {
        color: #ffffff;
        background-color: #ff007f; /* Rosa Neón */
        border-color: #ff409f;
        box-shadow: 0 0 15px rgba(255, 0, 127, 0.8); 
        transform: translateY(-2px);
    }
    button:active {
        transform: translateY(0);
    }
</style>