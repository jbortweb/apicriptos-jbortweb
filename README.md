# CryptoAPI - Cotizador de Criptomonedas

¡Bienvenidos a CryptoAPI! Esta aplicación permite consultar y cotizar diferentes criptomonedas en diversas monedas. Es una herramienta útil para mantenerse actualizado con los valores actuales de las criptomonedas más populares.

## Demo

Puedes ver la aplicación en acción [aquí](https://cryptoapijbortweb.netlify.app/).

## Tecnologías Utilizadas

- **Vue 3**: Framework progresivo de JavaScript para construir interfaces de usuario.
- **CryptoCompare API**: Fuente de datos para obtener las cotizaciones de criptomonedas.

## Características

- **Selección de Monedas**: Puedes seleccionar entre varias monedas (USD, MXN, EUR, GBP) para ver la cotización en la moneda de tu preferencia.
- **Listado de Criptomonedas**: Obtén una lista de las criptomonedas más populares y selecciona la que deseas cotizar.
- **Cotización en Tiempo Real**: Visualiza la cotización actual, el precio más alto y más bajo del día, y la variación en las últimas 24 horas.

## Instalación

Para ejecutar este proyecto localmente, sigue estos pasos:

1. Clona el repositorio:

   ```sh
   git clone https://github.com/jbortweb/apicriptos-jbortweb.git
   ```

2. Navega al directorio del proyecto:

   ```sh
   cd apicriptos-jbortweb
   ```

3. Instala las dependencias:

   ```sh
   npm install
   ```

4. Ejecuta la aplicación en modo desarrollo:

   ```sh
   npm run dev
   ```

5. Abre [http://localhost:5137](http://localhost:5137) en tu navegador para ver la aplicación.

## Uso

### Obteniendo Cotizaciones

1. Selecciona una moneda de la lista desplegable.
2. Selecciona una criptomoneda de la lista desplegable.
3. Haz clic en "Cotizar".
4. Visualiza los resultados, incluyendo el precio actual, el precio más alto y más bajo del día, y la variación en las últimas 24 horas.


## Código de Ejemplo

Aquí tienes un fragmento del código utilizado en el proyecto:

```javascript
import { ref, onMounted, computed } from "vue";

export default function useCrypto() {
  const criptomonedas = ref([]);
  const cotizacion = ref({});
  const cargando = ref(false);

  const monedas = ref([
    { codigo: "USD", texto: "Dolar de Estados Unidos" },
    { codigo: "MXN", texto: "Peso Mexicano" },
    { codigo: "EUR", texto: "Euro" },
    { codigo: "GBP", texto: "Libra Esterlina" },
  ]);

  onMounted(() => {
    const url =
      "https://min-api.cryptocompare.com/data/top/mktcapfull?limit=10&tsym=EUR";

    fetch(url)
      .then((res) => res.json())
      .then(({ Data }) => {
        criptomonedas.value = Data;
      });
  });

  const obtenerCotizacion = async (cotizar) => {
    cargando.value = true;
    cotizacion.value = {};
    try {
      const { moneda, criptomoneda } = cotizar;
      const url = `https://min-api.cryptocompare.com/data/pricemultifull?fsyms=${criptomoneda}&tsyms=${moneda}`;

      const res = await fetch(url);
      const data = await res.json();
      cotizacion.value = data.DISPLAY[criptomoneda][moneda];
    } catch (error) {
      console.log(error);
    } finally {
      cargando.value = false;
    }
  };

  const mostrarResultado = computed(() => {
    return Object.values(cotizacion.value).length > 0;
  });

  return {
    monedas,
    criptomonedas,
    obtenerCotizacion,
    cargando,
    cotizacion,
    mostrarResultado,
  };
}
```
### Contribuciones
¡Las contribuciones son bienvenidas! Si tienes alguna sugerencia o mejora, no dudes en hacer un fork del repositorio y enviar un pull request. También puedes abrir un issue para reportar errores o hacer preguntas.
### Licencia
Este proyecto está bajo la licencia MIT.

¡Gracias por visitar mis proyectos! 🚀