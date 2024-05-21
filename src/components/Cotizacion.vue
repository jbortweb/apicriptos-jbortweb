<script setup>
defineProps({
  cotizacion: {
    type:Object,
    required: true
  }
})
</script>

<template>
  <div class="contenedor-resultado">
      <h2>Cotización</h2>
      <div class="resultado">
        <img
          :src="`https://cryptocompare.com/${cotizacion.IMAGEURL}`"
          alt="logo criptomoneda"
        />
        <div>
          <p>
            El precio es de: <span>{{ cotizacion.PRICE }}</span>
          </p>
          <p>
            El precio más alto del día es de:
            <span>{{ cotizacion.HIGHDAY }}</span>
          </p>
          <p>
            El precio más bajo del día es de:
            <span>{{ cotizacion.LOWDAY }}</span>
          </p>
          <p>
            Variación últimas 24 horas:
            <span>{{ cotizacion.CHANGEPCT24HOUR }}%</span>
          </p>
          <p>
            Última actualización: <span>{{ cotizacion.LASTUPDATE }}</span>
          </p>
        </div>
      </div>
    </div>
</template>

<style scoped>
</style>