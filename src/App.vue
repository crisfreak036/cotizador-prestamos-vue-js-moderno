<script setup>
  import { ref, reactive } from 'vue';
  import Header from './components/Header.vue';

  // Definición de state con ref
  const cantidad = ref(10000);

  const MIN = 0;
  const MAX = 20000;
  const STEP = 100;

  const handleChange = (e) => {
    cantidad.value = +e.target.value;
  }
</script>

<template>
  <div
    class="my-20 max-w-lg mx-auto bg-white shadow p-10"
  >
    <Header/>

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
        @input="handleChange"
      />
    </div>

    <p
        class='text-center my-10 text-5xl font-extrabold text-indigo-600'
      >
        {{cantidad}}
    </p>
  </div>
</template>
