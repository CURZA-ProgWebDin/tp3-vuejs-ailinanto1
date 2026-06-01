<template>
    <div class="contenedor-lista">
        <div v-if="cargando">
            <h2>CARGANDO...</h2>
        </div>
        <div v-else ref="box" class="lista">
            <tarjetaProducto v-for="(prod, index) in productos" :key="prod.id">
                <template #header>
                    <h3>{{ prod.nombre }}</h3>
                </template>
                <template #body="{ expandido }">
                    <p>Precio: ${{ prod.precio }}</p>
                    <div v-if="expandido">
                        <p>Categorías: {{ prod.categoria }}</p>
                        <p>Stock: {{ prod.stock }}</p>
                    </div>
                </template>
                <template #footer="{ expandido, toggleExpandir }">
                    <button @click="toggleExpandir" class="btn-ver-mas">
                        {{ expandido ? 'Ver menos' : 'Ver más' }}
                    </button>
                    <button class="btn-comprar">
                        <svg viewBox="0 0 24 24" width="18" height="18" fill="currentColor" style="vertical-align: middle; margin-right: 5px;">
                            <path :d="mdiCart" />
                        </svg>
                        Comprar
                    </button>
                </template>
            </tarjetaProducto>
        </div>
    </div>
</template>
<script setup>
    import tarjetaProducto from './layouts/tarjetaProducto.vue';
    import { ref } from 'vue';
    import { onMounted } from 'vue';
    import { onUpdated } from 'vue';
    import { onBeforeUnmount } from 'vue';
    import { useTemplateRef } from 'vue';
    import { mdiCart } from '@mdi/js';

    const props = defineProps ({
        productos: {
            type: Array,
            required: true
        }
    })
    const cargando = ref(true)
    const box = useTemplateRef('box')
    let timer = null

    function esperar(ms) {
        return new Promise(resolve => setTimeout(resolve, ms))
    }

    async function cargarProductos() {
        cargando.value = true
        await esperar(800)
        cargando.value = false
    }

    onMounted( () => {
        cargarProductos()
        timer = setInterval(() => {
            cargarProductos()
        }, 30000)
    } )

    onUpdated(() => {
        if (box.value) {
            box.value.scrollTop = box.value.scrollHeight
        }
    })

    onBeforeUnmount(() => {
        clearInterval(timer)
        console.log('ListaProductos desmontado — polling detenido')
    })
</script>
<style scoped>
    .contenedor-lista h2 {
        color: #ffffff;
        text-align: center;
        font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; 
    }
    .lista {
        font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; 
        max-height: 500px;
        overflow-y: auto;  
        padding-right: 10px;
    }
    .lista::-webkit-scrollbar {
        width: 6px;
    }
    .lista::-webkit-scrollbar-track {
        background: #232329;
        border-radius: 10px;
    }
    .lista::-webkit-scrollbar-thumb {
        background: #ff007f;
        border-radius: 10px;
    }
    h3 {
        color: #ffffff;             
        font-weight: 700;
        text-align: center;
        margin-bottom: 8px;
        letter-spacing: 0.5px;
    }
    p {
        color: #e2e8f0;        
        font-size: 1rem;
        text-align: center;
        margin-top: 4px;
        margin-bottom: 12px;
    }
    .btn-comprar, .btn-ver-mas {
        width: 100%;      
        padding: 10px 16px;
        border-radius: 6px;
        font-weight: bold;
        font-size: 0.9rem;
        cursor: pointer;
        text-transform: uppercase;
        margin-top: 10px;   
        transition: all 0.25s ease-in-out;
        display: inline-block;
        text-align: center;
    }
    .btn-comprar {
        background-color: #ff007f;
        color: #ffffff;
        border: 2px solid #ff007f;
        box-shadow: 0 4px 10px rgba(255, 0, 127, 0.3);
    }
    .btn-comprar:hover {
        background-color: #ffffff;
        color: #ff007f;
        border-color: #ff2a93;
        box-shadow: 0 0 15px rgba(255, 0, 127, 0.8);
        transform: translateY(-2px);
    }
    .btn-ver-mas {
        background-color: rgba(255, 0, 127, 0.05);
        color: #ff007f;
        border: 2px solid #ff007f;
    }
    .btn-ver-mas:hover {
        background-color: #ffffff;
        color: #ff007f;
        border-color: #ffffff;
        box-shadow: 0 0 15px rgba(255, 255, 255, 0.5);
        transform: translateY(-2px);
    }    
    .btn-comprar:active, .btn-ver-mas:active {
        transform: translateY(0);
    }
</style>