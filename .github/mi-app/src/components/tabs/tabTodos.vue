<template>
    <ListaProductos :productos="productos"/>
</template>
<script setup>
    import { productos } from '../../data/productos.js';
    import ListaProductos from '../listaProductos.vue';
    import { onUnmounted, onMounted, onActivated,onDeactivated } from 'vue';

    onMounted( () => {
        console.log('tabTodos - Montado')
    })

    onUnmounted( () => {
        console.log('tabTodos - Desmontado')
    })

    onActivated( () => {
        console.log('tabTodos - Activado')
    })

    onDeactivated( () => {
        console.log('tabTodos - Desactivado')
    })
</script>