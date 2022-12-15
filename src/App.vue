<script setup>
  import { ref, watch } from 'vue';
  import Header from './components/Header.vue';
  import Button from './components/Button.vue';

  import { calcularTotalAPagar, formatearDinero } from './helpers/index.js'

  // Definición de state con ref
  const cantidad = ref(10000);
  const plazoPagar = ref(6);
  const total = ref(0)
  const totalMensual = ref(0)

  const MIN = 0;
  const MAX = 20000;
  const STEP = 100;

  watch([cantidad, plazoPagar], () => {
    total.value = calcularTotalAPagar(cantidad.value, plazoPagar.value)
    totalMensual.value = total.value/plazoPagar.value
  });

  const handleRange = (e) => {
    cantidad.value = +e.target.value;
  };

  const handleDecremento = (texto) => {
    console.log(texto)
    const valor = cantidad.value - STEP;
    if (valor < MIN) return alert('Cantidad no valida')
    cantidad.value = valor;
  };

  const handleIncremento = (texto) => {
    console.log(texto)
    const valor = cantidad.value + STEP;
    if (valor > MAX) return alert('Cantidad no valida')
    cantidad.value = valor;
  };

</script>

<template>
  <div
    class="my-20 max-w-lg mx-auto bg-white shadow p-10"
  >
    <Header/>

    <div
      className='flex justify-between my-6'
    >
      <Button
        :tipoBoton="'button'"
        :contenidoTexto="'-'"
        @handle="handleDecremento"
      />

      <Button
        :tipoBoton="'button'"
        :contenidoTexto="'+'"
        @handle="handleIncremento"
      />

    </div>

    <div class="my-5">
      <input 
        type="range" 
        name="" 
        id=""
        class='w-full h-6 bg-gray-200 accent-lime-500 hover:accent-lime-600 mt-5'
        :min="MIN"
        :max="MAX"
        :step="STEP"
        :value="cantidad"
        @input="handleRange"
      />
    </div>

    <p
        class='text-center my-10 text-5xl font-extrabold text-indigo-600'
      >
        {{formatearDinero(cantidad)}}
    </p>

    <h2 
        class='text-2xl font-extrabold text-gray-500 text-center'
      >
        Elige un <span class='text-indigo-600'>Plazo</span> a pagar
    </h2>

    <select
      class='mt-5 w-full p-2 bg-white border border-gray-300 rounded-lg text-center text-xl font-bold text-gray-500'
      v-model.number="plazoPagar"
    >
      <option value="6">6 Meses</option>
      <option value="12">12 Meses</option>
      <option value="24">24 Meses</option>
    </select>

    <div
        v-if="total > 0" 
        class="my-5 space-y-3 bg-gray-50 p-5 shadow"
      >
        <h2 class='text-2xl font-extrabold text-gray-500 text-center'>
          Resumen <span class='text-indigo-600'>de Pagos</span>
        </h2>

        <p 
          class="text-xl text-gray-500 text-center font-bold"
        >
          {{plazoPagar}} Meses
        </p>
        <p 
          class="text-xl text-gray-500 text-center font-bold"
        >
          Total a Pagar: {{formatearDinero(total)}}
        </p>
        <p 
          class="text-xl text-gray-500 text-center font-bold"
        >
          Pagos Mensuales: {{formatearDinero(totalMensual)}}
        </p>
    </div>

    <p v-else class="text-center pt-5 text-black font-bold"> Añade una cantidad y un plazo a pagar </p>
  </div>
</template>
