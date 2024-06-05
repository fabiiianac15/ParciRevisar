<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gray-100">
    <h1 class="text-2xl font-bold mb-4 text-center">Bandeja de entrada</h1>
    <div class="space-y-4 w-full max-w-md">
      <div
        v-for="correo in correos"
        :key="correo.id"
        class="correo bg-white p-4 flex flex-col justify-between items-start cursor-pointer rounded-lg shadow-md"
        :class="{
          'border-4 border-blue-500': correo.selected,
          'border-4 border-blue-300': correo.hovered && !correo.selected
        }"
        @click="seleccionarCorreo(correo)"
        @mouseover="correo.hovered = true"
        @mouseleave="correo.hovered = false"
      >
        <!-- Icono de estado -->
        <div class="flex items-center mb-2">
          <CheckIcon v-if="correo.leido" class="h-6 w-6 text-green-500 mr-2" />
        </div>
        <!-- Resto del contenido de la caja -->
        <div class="text-left w-full">
          <p :class="{ 'font-bold': !correo.leido, 'font-normal': correo.leido }">{{ correo.titulo }}</p>
          <p class="text-gray-500 text-sm">{{ correo.texto }}</p>
          <p class="text-gray-400 text-xs">{{ correo.tiempo }}</p>
        </div>
        <button
          v-if="correo.selected && !correo.leido"
          class="text-blue-500 text-sm self-start mt-2"
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
import { ExclamationCircleIcon, CheckIcon, XMarkIcon } from '@heroicons/vue/24/solid';

const correos = ref([
  { id: 'correo1', titulo: 'Correo 1', texto: 'Texto del correo 1', tiempo: 'Hace 1 hora', leido: false, selected: false, hovered: false, emergencia: true, eliminado: false },
  { id: 'correo2', titulo: 'Correo 2', texto: 'Texto del correo 2', tiempo: 'Hace 1 hora', leido: false, selected: false, hovered: false, emergencia: false, eliminado: false },
  { id: 'correo3', titulo: 'Correo 3', texto: 'Texto del correo 3', tiempo: 'Hace 2 horas', leido: false, selected: false, hovered: false, emergencia: false, eliminado: true },
  { id: 'correo4', titulo: 'Correo 4', texto: 'Texto del correo 4', tiempo: 'Ayer', leido: false, selected: false, hovered: false, emergencia: true, eliminado: false },
]);

function seleccionarCorreo(correo) {
  correo.selected = !correo.selected;
}

function marcarLeido(correo) {
  correo.leido = true;
  correo.selected = false;
}
</script>

