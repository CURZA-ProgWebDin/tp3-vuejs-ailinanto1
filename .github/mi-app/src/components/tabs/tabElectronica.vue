<template>
    <listaProductos :productos="productosFiltrados"/>
</template>
<script setup>
    import { productos } from '../../data/productos.js';
    import listaProductos from '../listaProductos.vue';
    import { onUnmounted, onMounted, onActivated,onDeactivated } from 'vue';

    const productosFiltrados = productos.filter(prod => prod.categoria === 'Electrónica');

    onMounted( () => {
        console.log('tabElectronica - Montado')
    })

    onUnmounted( () => {
        console.log('tabElectronica - Desmontado')
    })

    onActivated( () => {
        console.log('tabElectronica - Activado')
    })

    onDeactivated( () => {
        console.log('tabElectronica - Desactivado')
    })
</script>