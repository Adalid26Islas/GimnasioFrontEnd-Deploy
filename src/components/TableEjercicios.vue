<template>
  <div class="overflow-x-auto mt-4">
    <table class="min-w-full divide-y divide-gray-200 bg-white dark:bg-gray-800 max-w-screen-lg mx-auto">
      <thead class="bg-gray-900 text-white dark:bg-gray-700">
        <tr>
          <th class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider">#</th>
          <th class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider">Video</th>
          <th class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider">Nombre</th>
          <th class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider">Descripción</th>
          <th class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider">Tipo</th>
          <th class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider">Estatus</th>
          <th class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider">Dificultad</th>
          <th class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider">Fecha Registro</th>
          <th class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider">Fecha Actualización</th>
          <th class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider">Recomendaciones</th>
          <th class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider">Restricciones</th>
          <th class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider">Eliminar</th>
          <th class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider">Editar</th>
        </tr>
      </thead>
      <tbody class="bg-white divide-y divide-gray-200 dark:bg-gray-800 dark:divide-gray-700">
        <tr v-for="(ejercicio, index) in ejercicios" :key="index">
          <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900 dark:text-white">{{ index + 1 }}</td>
          <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 dark:text-gray-400">
            <a :href="ejercicio.video" target="_blank">Ver Video</a>
          </td>
          <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900 dark:text-white">{{ ejercicio.nombre }}</td>
          <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 dark:text-gray-400">{{ ejercicio.descripcion }}</td>
          <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 dark:text-gray-400">{{ ejercicio.tipo }}</td>
          <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 dark:text-gray-400">{{ ejercicio.estatus }}</td>
          <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 dark:text-gray-400">{{ ejercicio.dificultad }}</td>
          <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 dark:text-gray-400">{{ ejercicio.fechaRegistro }}</td>
          <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 dark:text-gray-400">{{ ejercicio.fechaActualizacion }}</td>
          <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 dark:text-gray-400">{{ ejercicio.recomendaciones }}</td>
          <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 dark:text-gray-400">{{ ejercicio.restricciones }}</td>
          <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-red-600 dark:text-red-400"><a href="#">Eliminar</a></td>
          <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-blue-600 dark:text-blue-400"><a href="#">Editar</a></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    ejercicios: Array
  }
};
</script>

<style scoped>
/* Agrega tus estilos aquí */
</style>
