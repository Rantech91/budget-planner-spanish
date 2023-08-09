<script setup>
import { computed } from "vue";
import CircleProgress from "vue3-circle-progress-bar";
import "vue3-circle-progress-bar/dist/circle-progress-bar.css";
import { formatearCantidad } from "../helpers";

const props = defineProps({
  presupuesto: {
    type: Number,
    required: true,
  },
  disponible: {
    type: Number,
    required: true,
  },
  gastado: {
    type: Number,
    required: true,
  },
});
const emits = defineEmits(["reset-app"]);

const porcentajeGastado = computed(() => {
  if (props.presupuesto) {
    return (props.gastado * 100) / props.presupuesto;
  }
  return 50;
});
console.log(porcentajeGastado);
</script>

<template>
  <div class="dos-columnas">
    <div class="contenedor-grafico">
      <p class="porcentaje">{{ porcentajeGastado }}%</p>
      <CircleProgress
        :percent="porcentajeGastado"
        :size="250"
        :border-width="30"
        :border-bg-width="30"
        fill-color="#3b82f6"
        empty-color="#CDCDCD"
      />
    </div>
    <div class="contenedor-presupuesto">
      <button type="button" class="reset-app" @click="emits('reset-app')">
        Resetear App
      </button>
      <p>
        <span>Presupuesto:</span>
        {{ formatearCantidad(presupuesto) }}
      </p>
      <p>
        <span>Disponible:</span>
        {{ formatearCantidad(disponible) }}
      </p>
      <p>
        <span>Gastado:</span>
        {{ formatearCantidad(gastado) }}
      </p>
    </div>
  </div>
</template>

<style scoped>
.contenedor-grafico {
  position: relative;
  display: flex;
  justify-content: center;
}
.porcentaje {
  position: absolute;

  margin: auto;
  top: calc(50% - 1.5rem);
  left: 0;
  right: 0;
  text-align: center;
  font-weight: 900;
  z-index: 10;
  font-size: 3rem;
  color: var(--gris-oscuro);
}
.dos-columnas {
  display: flex;
  flex-direction: column;
}
.dos-columnas > :first-child {
  margin-bottom: 3rem;
}
@media (min-width: 768px) {
  .dos-columnas {
    flex-direction: row;
    gap: 4rem;
    align-items: center;
  }
  .dos-columnas > :first-child {
    margin-bottom: 0rem;
  }
}

.reset-app {
  background-color: #db2777;
  border: none;
  padding: 1.5rem;
  width: 100%;
  color: var(--blanco);
  font-weight: 900;
  text-transform: uppercase;
  border-radius: 1rem;
  transition-property: background-color;
  transition-duration: 300ms;
  letter-spacing: 1.5px;
}
.reset-app:hover {
  cursor: pointer;
  background-color: #ba2367;
}
.contenedor-presupuesto {
  width: 100%;
}
.contenedor-presupuesto p {
  font-size: 2.4rem;
  text-align: center;
  color: var(--gris-oscuro);
}

@media (min-width: 768px) {
  .contenedor-presupuesto p {
    text-align: left;
  }
}
.contenedor-presupuesto span {
  font-weight: 900;
  color: var(--azul);
}
</style>
