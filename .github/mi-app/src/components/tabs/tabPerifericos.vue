<template>
    <listaProductos :productos="productosFiltrados"/>
</template>
<script setup>
    import { productos } from '../../data/productos.js';
    import listaProductos from '../listaProductos.vue';
    import { onUnmounted, onMounted, onActivated,onDeactivated } from 'vue';

    const productosFiltrados = productos.filter(prod => prod.categoria === 'Periféricos');

    onMounted( () => {
        console.log('tabPerifericos - Montado')
    })

    onUnmounted( () => {
        console.log('tabPerifericos - Desmontado')
    })

    onActivated( () => {
        console.log('tabPerifericos - Activado')
    })

    onDeactivated( () => {
        console.log('tabPerifericos - Desactivado')
    })
</script>