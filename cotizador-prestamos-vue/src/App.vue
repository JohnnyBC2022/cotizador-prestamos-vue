<script setup>
import { ref, computed } from 'vue';
import Header from './components/Header.vue';
import Button from './components/Button.vue';

const cantidad = ref(10000);
const MIN = 0;
const MAX = 20000;
const STEP = 100;

/* function handleChange(e) {
  cantidad.value = Number(e.target.value); // por defecto te pone la cantidad como string. al eliminarla podemos usar el v-model
} */

const formatearDinero = computed(() => {
  const formatter = new Intl.NumberFormat('es-ES', {
    style: 'currency',
    currency: 'EUR'
  })

  return formatter.format(cantidad.value)
});

const handleChangeDecremento = () => {
  const valor = cantidad.value - STEP
  if(valor < MIN) {
    alert('Cantidad no válida')
    return;
  }
  cantidad.value = valor;
}

const handleChangeIncremento = () => {
  const valor = cantidad.value + STEP
  if(valor > MAX) {
    alert('Cantidad no válida')
    return;
  }
  cantidad.value = valor;
}

</script>

<!--
hay una variante a Options API
que es composition API su sintaxis sería
<script>
impor Header from './components/Header.vue'

export default {
 components: {
  Header
 }
}
<script>
-->

<template>
  <div class="my-20 max-w-lg mx-auto bg-white shadow p-10">
    <Header />

    <div class="flex justify-between mt-10">
      <Button
      :operador="'-'"
      :fn="handleChangeDecremento"
      />
      <Button
      :operador="'+'"
      :fn="handleChangeIncremento"
      />
      
    </div>
    <div class="my-5">
      <input type="range" class="w-full bg-gray-200 accent-lime-500 hover:accent-lime-600"
      :min="MIN"
      :max="MAX"
      :step="STEP"
      v-model.number="cantidad"
      >
      <!-- el @ es un evento en vue el evento sería un v-on: -->
      <p class="text-center my-10 text-5xl font-extrabold text-indigo-600">
        {{ formatearDinero }}
      </p>
    </div>
  </div>
</template>
