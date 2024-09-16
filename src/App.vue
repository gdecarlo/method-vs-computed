<template>
  <div>
    <h1>Comparar Método vs Computado</h1>

    <!-- Mostrar la suma usando una propiedad computada -->
    <p>Computado: {{ sumaComputada }}</p>

    <!-- Mostrar la suma usando un método -->
    <p>Método: {{ calcularSumaMetodo() }}</p>

    <!-- Botón para agregar un número -->
    <button @click="agregarNumero">Agregar número</button>
    <p>Números: {{ numeros }}</p>

    <!-- Nueva acción: Cambiar el estado de un valor no relacionado -->
    <button @click="cambiarEstado">Cambiar Estado (el DOM se actualiza)</button>
    <p>Estado no relacionado: {{ estadoNoRelacionado }}</p>
  </div>
</template>

<script setup>
import { ref, computed,onUpdated  } from 'vue'


onUpdated (() => {
  console.log('Se actualiza el DOM...')
})
// Estado
const numeros = ref([1, 2, 3, 4, 5])
const estadoNoRelacionado = ref('Inicial')

// Método para sumar los números
const calcularSumaMetodo = () => {
  console.log('Método: Se ejecuta cada vez que es llamado.')
  return numeros.value.reduce((acc, num) => acc + num, 0)
}

// Propiedad computada para sumar los números
const sumaComputada = computed(() => {
  console.log('Computado: Solo se recalcula si "numeros" cambia.')
  return numeros.value.reduce((acc, num) => acc + num, 0)
})

// Método para agregar un número aleatorio
const agregarNumero = () => {
  const nuevoNumero = Math.floor(Math.random() * 10) + 1
  numeros.value.push(nuevoNumero)
}

// Método para cambiar el estado no relacionado
const cambiarEstado = () => {
  estadoNoRelacionado.value = estadoNoRelacionado.value === 'Inicial' ? 'Cambiado' : 'Inicial'
}
</script>
