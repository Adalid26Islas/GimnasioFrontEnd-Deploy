<template>
  <div class="container mx-auto p-4">
    <!-- Botón para mostrar/ocultar formulario y botón de registrar -->
    <div class="mb-4 flex justify-center space-x-4">
      <button @click="mostrarFormulario = !mostrarFormulario" class="px-4 py-2 rounded bg-red-600 text-white hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-red-500 transition-colors">
        {{ mostrarFormulario ? 'Ocultar' : 'Registrar' }} Ejercicio
      </button>
      <button v-if="mostrarFormulario" type="submit" class="px-4 py-2 rounded bg-red-600 text-white hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-red-500 transition-colors">
        Registrar
      </button>
    </div>

    <!-- Formulario -->
    <div v-if="mostrarFormulario" class="flex flex-col gap-4">
      <form class="bg-gray-900 dark:bg-gray-700 shadow rounded-lg p-6 grid grid-cols-1 md:grid-cols-2 gap-4">
        <!-- Columna 1 -->
        <div class="space-y-4">
          <div>
            <label for="nombre" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Nombre Completo</label>
            <input type="text" name="nombre" id="nombre" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" placeholder="Nombre Completo" required>
          </div>
          <div>
            <label for="primerApellido" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Primer Apellido</label>
            <input type="text" name="primerApellido" id="primerApellido" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" placeholder="Primer Apellido" required>
          </div>
          <div>
            <label for="segundoApellido" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Segundo Apellido</label>
            <input type="text" name="segundoApellido" id="segundoApellido" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" placeholder="Segundo Apellido" required>
          </div>
          <div>
            <label for="genero" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Genero</label>
            <select id="genero" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" required>
              <option value="" disabled selected>Selecciona Genero</option>
              <option value="M">Masculino</option>
              <option value="F">Femenino</option>
              <option value="NB">No Binario</option>
            </select>
          </div>
          <div>
            <label for="sangre" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Tipo de Sangre</label>
            <select id="sangre" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" required>
              <option value="" disabled selected>Selecciona Tipo de Sangre</option>
              <option value="A+">A+</option>
              <option value="A-">A-</option>
              <option value="B+">B+</option>
              <option value="B-">B-</option>
              <option value="AB+">AB+</option>
              <option value="AB-">AB-</option>
              <option value="O+">O+</option>
              <option value="O-">O-</option>
            </select>
          </div>
        </div>

        <!-- Columna 2 -->
        <div class="space-y-4">
          <div>
            <label for="fechaNacimiento" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Fecha de Nacimiento</label>
            <input type="date" name="fechaNacimiento" id="fechaNacimiento" class="p-2 rounded-lg w-full bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
          </div>
          <div>
            <label for="foto" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Fotografía</label>
            <input type="file" name="foto" id="foto" class="p-2 rounded-lg w-full bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
          </div>
        </div>
      </form>
    </div>

    <!-- Botón de enviar -->
    <div class="mt-4">
      <button
        type="submit"
        class="w-full px-4 py-2 rounded-lg bg-red-600 text-white hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-red-500 transition-colors"
      >
        <svg class="w-6 h-6 inline-block mr-2" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M16 21v-2a4 4 0 00-4-4H5a4 4 0 00-4 4v2" />
          <circle cx="8.5" cy="7" r="4" />
          <path d="M20 8v6M23 11h-6" />
        </svg>
        <span class="uppercase">Registrar</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mostrarFormulario: false,  // Estado que controla la visibilidad del formulario
    };
  },
};
</script>
