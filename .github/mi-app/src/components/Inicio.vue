<template>
    <div class="contenedor-columnas">
        <TarjetaProducto class="tarjeta-individual">
            <template #header>
                <h3>{{ prods[0].nombre }}</h3>
                <p>Categorías: {{ prods[0].categoria }}</p>
            </template>
            <template #body="{ expandido }">
                <div v-if="expandido">
                    <p>Precio: ${{ prods[0].precio }}</p>
                    <p>Stock: {{ prods[0].stock }}</p>
                </div>
            </template>
            <template #footer="{ expandido, toggleExpandir }">
                <button @click="toggleExpandir" class="btn-ver-mas">
                    {{ expandido ? 'Ver menos' : 'Ver más' }}
                </button>
                <button class="btn-comprar">
                    <svg viewBox="0 0 24 24" width="18" height="18" fill="currentColor"
                        style="vertical-align: middle; margin-right: 5px;">
                        <path :d="mdiCart" />
                    </svg>
                    Comprar
                </button>
            </template>
        </TarjetaProducto>
        <TarjetaProducto class="tarjeta-individual">
            <template #header>
                <h3>{{ prods[1].nombre }}</h3>
                <p>Categorías: {{ prods[1].categoria }}</p>
            </template>
            <template #body="{ expandido, toggleExpandir }">
                <div v-if="expandido">
                    <p>Stock: {{ prods[1].stock }}</p>
                    <p>Precio: ${{ prods[1].precio }}</p>
                </div>
            </template>
            <!--<template #footer="{ expandido, toggleExpandir }">
                <button @click="toggleExpandir" class="btn-ver-mas">
                    {{ expandido ? 'Ver menos' : 'Ver más' }}
                </button>
                <button class="btn-comprar">
                    <svg viewBox="0 0 24 24" width="18" height="18" fill="currentColor"
                        style="vertical-align: middle; margin-right: 5px;">
                        <path :d="mdiCart" />
                    </svg>
                    Comprar
                </button>
            </template>-->
        </TarjetaProducto>
        <TarjetaProducto class="tarjeta-individual tarjeta-destacada">
            <template #header>
                <h3 class="titulo-rayos">
                    <svg viewBox="0 0 24 24" width="22" height="22" fill="currentColor" class="icono-rayo">
                        <path :d="mdiLightningBolt" />
                    </svg>
                    {{ prods[2].nombre }}
                    <svg viewBox="0 0 24 24" width="22" height="22" fill="currentColor" class="icono-rayo">
                        <path :d="mdiLightningBolt" />
                    </svg>
                </h3>
                <p>Categorías: {{ prods[2].categoria }}</p>
            </template>
            <template #body="{ expandido }">
                <p style="color: #ff007f; font-weight: bold;">¡50% OFF LIQUIDACIÓN!</p>
                <p>Precio Oferta: ${{ prods[2].precio / 2 }}</p>
                <div v-if="expandido">
                    <p>Stock disponible: {{ prods[2].stock }} un.</p>
                    <p>Código exclusivo: <span style="color: #00ffcc; font-weight: bold;">NEON50</span></p>
                </div>
            </template>
            <template #footer="{ expandido, toggleExpandir }">
                <button @click="toggleExpandir" class="btn-ver-mas">
                    {{ expandido ? 'Ocultar Cupón' : 'Ver Cupón' }}
                </button>
                <button class="btn-comprar btn-cupon">
                    Reclamar Cupón
                </button>
            </template>
        </TarjetaProducto>
    </div>
</template>
<script setup>
import TarjetaProducto from './layouts/tarjetaProducto.vue';
import { productos } from '../data/productos.js';
import { mdiCart, mdiLightningBolt } from '@mdi/js';

const prods = productos;
</script>
<style scoped>
/* Contenedor principal que alinea tus tres tarjetas en una fila horizontal */
.contenedor-columnas {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: flex-start;
    gap: 25px;
    /* Espacio entre cada tarjeta */
    padding: 30px;
    width: 100%;
    box-sizing: border-box;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

/* Forzamos a que las tarjetas usen el look oscuro de tu app y se repartan el ancho */
.tarjeta-individual {
    flex: 1;
    min-width: 280px;
    max-width: 360px;
    background-color: #232329 !important;
    /* El color oscuro de fondo */
    border-radius: 12px !important;
    padding: 20px !important;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.4) !important;
    border: none !important;
}

/* Alineación interna de los textos y títulos */
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

/* Estilo para los rayos de la tercera tarjeta */
.titulo-rayos {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
}

.icono-rayo {
    color: #ff007f;
    /* Los rayos ahora brillan en fucsia */
    filter: drop-shadow(0 0 5px rgba(255, 0, 127, 0.5));
}

/* Opcional: una sutil distinción de borde para la tarjeta destacada */
.tarjeta-destacada {
    border: 1px dashed rgba(255, 0, 127, 0.3) !important;
}

/* === DISEÑO DE TUS BOTONES ORIGINALES (Unificados) === */
.btn-comprar,
.btn-ver-mas {
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

.btn-comprar:active,
.btn-ver-mas:active {
    transform: translateY(0);
}

/* === NUEVO ESTILO PARA EL BOTÓN DE CUPÓN (.btn-cupon) === */
/* Eliminamos el turquesa y le damos un look que combina perfecto con el fucsia */
.btn-cupon {
    background-color: transparent !important;
    color: #ff007f !important;
    border: 2px dashed #ff007f !important;
    /* Borde discontinuo para denotar que es un cupón troquelado */
    box-shadow: none !important;
}

.btn-cupon:hover {
    background-color: #ff007f !important;
    color: #ffffff !important;
    border-style: solid !important;
    box-shadow: 0 0 15px rgba(255, 0, 127, 0.6) !important;
    transform: translateY(-2px);
}

/* Centrado automático del texto "Sin acciones disponibles" del footer (Instancia 2) */
:deep(footer span) {
    display: block;
    text-align: center;
    color: #8a8a98;
    font-size: 0.95rem;
    font-style: italic;
    padding: 10px 0;
}
</style>