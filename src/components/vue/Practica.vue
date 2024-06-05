<template>
    <div class="container mx-auto p-4">
      <h1 class="text-2xl font-bold mb-4">Bandeja de entrada</h1>
      <div class="space-y-4">
        <div
          v-for="(correo, index) in correos"
          :key="index"
          class="correo bg-white p-4 flex justify-between items-center cursor-pointer"
          :class="{ 'border-l-4 border-blue-500': correo.selected }"
          @click="seleccionarCorreo(correo)"
        >
          <div>
            <p class="font-bold">{{ correo.titulo }}</p>
            <p class="text-gray-500">{{ correo.texto }}</p>
            <p class="text-gray-400 text-sm">{{ correo.tiempo }}</p>
          </div>
          <button
            v-if="correo.selected && !correo.leido"
            class="text-blue-500"
            @click.stop="marcarLeido(correo)"
          >
            Marcar como leído
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const correos = ref([
    { id: 'correo1', titulo: 'Correo 1', texto: 'Texto del correo 1', tiempo: 'Hace 1 hora', leido: false, selected: false },
    { id: 'correo2', titulo: 'Correo 2', texto: 'Texto del correo 2', tiempo: 'Hace 1 hora', leido: false, selected: false },
    { id: 'correo3', titulo: 'Correo 3', texto: 'Texto del correo 3', tiempo: 'Hace 2 horas', leido: false, selected: false },
    { id: 'correo4', titulo: 'Correo 4', texto: 'Texto del correo 4', tiempo: 'Ayer', leido: false, selected: false },
  ]);
  
  function seleccionarCorreo(correo) {
    correo.selected = !correo.selected;
  }
  
  function marcarLeido(correo) {
    correo.leido = true;
    correo.selected = false;
  }
  </script>