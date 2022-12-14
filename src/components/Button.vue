<script setup>
    // const { tipoBoton, contenidoTexto, handle } = defineProps(['tipoBoton', 'contenidoTexto', 'handle'])
    const props = defineProps({
        tipoBoton: String, 
        contenidoTexto: String, 
        handle: Function
    })
</script>

<template>
    <button
        :type="tipoBoton"
        className='h-10 w-10 flex items-center justify-center font-bold text-white text-2xl bg-lime-500 rounded-full hover:ring-2 hover:ring-offset-2 hover:ring-lime-500'
        @click="handle"
    >
    {{contenidoTexto}}
    </button>
</template>