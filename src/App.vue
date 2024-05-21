<script setup>
import { reactive,ref } from "vue";
import Alerta from "./components/Alerta.vue";
import Spiner from "./components/Spiner.vue";
import useCrypto from './composables/useCrypto'
import Cotizacion from "./components/Cotizacion.vue";

const {monedas,criptomonedas,obtenerCotizacion,cargando,cotizacion,mostrarResultado} = useCrypto()

const cotizar = reactive({
    moneda: "",
    criptomoneda: "",
  });

  const error = ref("");

const cotizarCripto = () => {
    if (Object.values(cotizar).includes("")) {
      error.value = "Todos los campos son obligatorios";
      return;
    }
    error.value = "";
    obtenerCotizacion(cotizar);
  };
</script>

<template>
  <div class="contenedor">
    <h1 class="titulo">Cotizador de<span>Criptomonedas</span></h1>
  </div>
  <div class="contenido">
    <Alerta v-if="error">{{ error }}</Alerta>
    <form class="formulario" @submit.prevent="cotizarCripto">
      <div class="campo">
        <label for="moneda">Moneda:</label>
        <select id="moneda" v-model="cotizar.moneda">
          <option value="">-- Selecciona --</option>
          <option
            v-for="(moneda, i) in monedas"
            :key="i"
            :value="moneda.codigo"
          >
            {{ moneda.texto }}
          </option>
        </select>
      </div>
      <div class="campo">
        <label for="cripto">Criptomoneda:</label>
        <select id="cripto" v-model="cotizar.criptomoneda">
          <option value="">-- Selecciona --</option>
          <option
            v-for="(criptomoneda, i) in criptomonedas"
            :key="i"
            :value="criptomoneda.CoinInfo.Name"
          >
            {{ criptomoneda.CoinInfo.FullName }}
          </option>
        </select>
      </div>
      <input type="submit" value="Cotizar" />
    </form>
    <Spiner v-if="cargando" />
    <Cotizacion
      v-if="mostrarResultado"
      :cotizacion="cotizacion"
    ></Cotizacion>
  </div>
</template>