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
            <label for="nombre" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Nombre</label>
            <input type="text" name="nombre" id="nombre" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" placeholder="Nombre" required>
          </div>
          <div>
            <label for="descripcion" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Descripción</label>
            <input type="text" name="descripcion" id="descripcion" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" placeholder="Descripción" required>
          </div>
          <div>
            <label for="video" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Video</label>
            <input type="file" name="video" id="video" class="p-2 rounded-lg w-full bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
          </div>
          <div>
            <label for="tipo" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Tipo</label>
            <select id="tipo" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" required>
              <option>Selecciona Tipo</option>
              <option>Aeróbico</option>
              <option>Resistencia</option>
              <option>Flexibilidad</option>
              <option>Fuerza</option>
            </select>
          </div>
           <div>
            <label for="estatus" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Estatus</label>
            <select id="estatus" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" required>
              <option>Selecciona Estatus</option>
              <option>Activo</option>
              <option>Inactivo</option>
            </select>
          </div>
        </div>

        <!-- Columna 2 -->
        <div class="space-y-4">
         
          <div>
            <label for="dificultad" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Dificultad</label>
            <select id="dificultad" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" required>
              <option>Selecciona Dificultad</option>
              <option>Básico</option>
              <option>Intermedio</option>
              <option>Avanzado</option>
            </select>
          </div>
          <div>
            <label for="fechar" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Fecha de Registro</label>
            <input type="date" name="fechar" id="fechar" class="p-2 rounded-lg w-full bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
          </div>
          <div>
            <label for="fechaa" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Fecha de Actualización</label>
            <input type="date" name="fechaa" id="fechaa" class="p-2 rounded-lg w-full bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
          </div>
          <div>
            <label for="recomendaciones" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Recomendaciones</label>
            <input type="text" name="recomendaciones" id="recomendaciones" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" placeholder="Recomendaciones" required>
          </div>
          <div>
            <label for="restricciones" class="block text-sm font-medium text-gray-100 dark:text-gray-100">Restricciones</label>
            <input type="text" name="restricciones" id="restricciones" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" placeholder="Restricciones" required>
          </div>
        </div>
      </form>
    </div>

    <!-- Lista de ejercicios -->
    <div class="mt-4">
      <TableEjercicios />
    </div>
  </div>
</template>

<script>
import TableEjercicios from '../../components/TableEjercicios.vue';
export default {
  components: {
    TableEjercicios,
  },
  data() {
    return {
      mostrarFormulario: false,  // Estado que controla la visibilidad del formulario
    };
  },
};
</script>
