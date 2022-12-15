<script setup>
  import { ref, computed } from 'vue';
  import Header from './components/Header.vue';
  import Button from './components/Button.vue';

  // Definición de state con ref
  const cantidad = ref(10000);
  const plazoPagar = ref(6);

  const MIN = 0;
  const MAX = 20000;
  const STEP = 100;

  const formatearDinero = computed( () => {
    const formatter = new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD'
    });
    return formatter.format(cantidad.value);
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
        {{formatearDinero}}
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
  </div>
</template>
