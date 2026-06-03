<template>
    <div class="contenedor-tarjeta">
        <header>
            <slot name="header"></slot>
        </header>
        <main>
            <slot name="body" :expandido="estaExpandido"></slot>
        </main>
        <footer>
            <slot name="footer" :expandido="estaExpandido" :toggleExpandir="toggleExpandir">
                <span>Sin acciones disponibles</span>
            </slot>
        </footer>
    </div>
</template>
<script setup>
    import { ref } from 'vue';

    const estaExpandido = ref(false)
    const toggleExpandir = () => {
        estaExpandido.value = !estaExpandido.value
    }
</script>