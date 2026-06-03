<template>
    <div class="contenedor-paneles">
        <div class="seccion-normal">
            <h3>Componente sin KeepAlive</h3>
            <button @click="tabActivo = 'tabTodos'">Todos</button>
            <button @click="tabActivo = 'tabElectronica'">Electronica</button>
            <button @click="tabActivo = 'tabPerifericos'">Periféricos</button>
            <component :is="componentes[tabActivo]"/>

        </div>
        <div class="seccion-keepAlive">
            <h3>componente con KeepAlive</h3>
            <button @click="tabActivoConKeepAlive = 'tabTodos'">Todos</button>
            <button @click="tabActivoConKeepAlive = 'tabElectronica'">Electronica</button>
            <button @click="tabActivoConKeepAlive = 'tabPerifericos'">Periféricos</button>
            <KeepAlive>
                <component :is="componentes[tabActivoConKeepAlive]"/>
            </KeepAlive>
        </div>
    </div>
</template>
<script setup>
import { ref } from 'vue';
import tabTodos from './tabs/tabTodos.vue'
import tabElectronica from './tabs/tabElectronica.vue'
import tabPerifericos from './tabs/tabPerifericos.vue';

const tabActivo = ref('tabTodos')
const tabActivoConKeepAlive = ref('tabTodos')

const componentes = {
    tabTodos,
    tabElectronica,
    tabPerifericos
}
/**
    La implementación de KeepAlive resulta ideal para optimizar el rendimiento de la aplicación
    cuando los datos ya fueron recuperados, evitando redundancia en las peticiones al servidor.
    Al preservar el estado interno del componente en memoria, prevenimos que se destruya y se vuelva
    a instanciar al navegar por las pestañas.
    Por el contrario, si la información de la base de datos es altamente dinámica y requiere actualizaciones
    en tiempo real, es preferible omitir KeepAlive para asegurar que cada montaje traiga consigo el estado
    más reciente del backend.
*/
</script>
<style scoped>
h3 {
    color: #ffffff;
    font-weight: 700;
    text-align: center;
    margin-bottom: 8px;
    letter-spacing: 0.5px;
}
.contenedor-paneles {
    display: table;
    width: 100%;
    table-layout: fixed;
    border-collapse: separate;
    border-spacing: 20px;
    margin-top: 10px;
}

.seccion-normal,
.seccion-keepAlive {
    display: table-cell;
    vertical-align: top;
    background-color: #232329;
    border: 1px solid #454552;
    border-radius: 12px;
    padding: 20px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
}

button {
    background-color: #000000;
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
    background-color: #ff007f;
    /* Rosa Neón */
    border-color: #ff409f;
    box-shadow: 0 0 15px rgba(255, 0, 127, 0.8);
    transform: translateY(-2px);
}

button:active {
    transform: translateY(0);
}
</style>