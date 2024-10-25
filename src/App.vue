<script setup lang="ts">
import { BookOpenIcon } from 'lucide-vue-next'

interface DropEvent extends DragEvent {
  dataTransfer: DataTransfer;
}

const emit = defineEmits<{
  (e: 'fileDropped', file: File): void
}>()

const handleDrop = (event: DropEvent): void => {
  const file = event.dataTransfer.files[0]
  if (file && file.type === 'application/epub+zip') {
    emit('fileDropped', file)
    console.log('Archivo EPUB recibido:', file.name)
  } else {
    alert('Por favor, arrastra un archivo EPUB válido.')
  }
}
</script>

<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-900">
    <div class="text-center">
      <BookOpenIcon class="w-24 h-24 mx-auto mb-6 text-gray-300" />
      <h1 class="text-2xl font-semibold text-white mb-4">Lector de EPUB</h1>
      <p class="text-gray-400 max-w-md mx-auto">
        Arrastra y suelta tu archivo EPUB aquí para comenzar la lectura
      </p>
      <div
          class="mt-8 border-4 border-dashed border-gray-700 rounded-lg p-12 transition-colors duration-300 ease-in-out hover:border-gray-500"
          @dragover.prevent
          @drop.prevent="handleDrop"
      >
        <p class="text-gray-500">
          Suelta tu archivo EPUB aquí
        </p>
      </div>
    </div>
  </div>
</template>

