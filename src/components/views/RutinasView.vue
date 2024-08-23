<template>
  <div class="mx-auto p-4">
    <!-- Botón para mostrar el formulario -->
    <button
      v-if="!showForm"
      @click="toggleForm"
      class="px-4 py-2 mb-4 rounded bg-blue-600 text-white hover:bg-blue-700 focus:outline-none transition-colors"
    >
      Crear Rutina
    </button>

    <!-- Sección del Formulario -->
    <section v-if="showForm" class="mb-8 p-4 bg-white rounded shadow">
      <h1 class="text-xl font-semibold mb-4 text-gray-900">
        {{ isEditing ? "Actualizar Rutina" : "Crear nueva Rutina" }}
      </h1>
      <p class="text-gray-700 mb-6">
        {{
          isEditing
            ? "Actualiza la información de la rutina seleccionada."
            : "Ingresa la información correspondiente para crear una nueva rutina."
        }}
      </p>

      <form @submit.prevent="submitForm">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
          <input
            v-model="formData.Nombre"
            type="text"
            placeholder="Nombre de la Rutina"
            class="p-2 rounded-lg w-full bg-gray-100 border border-gray-300 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
            required
          />
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
          <input
            v-model="formData.Programa_Saludable_ID"
            type="number"
            placeholder="Programa Saludable ID"
            class="p-2 rounded-lg w-full bg-gray-100 border border-gray-300 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
            required
          />
          <input
            v-model="formData.Tiempo_Aproximado"
            type="text"
            placeholder="Tiempo Aproximado"
            class="p-2 rounded-lg w-full bg-gray-100 border border-gray-300 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
            required
          />
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
          <select
            v-model="formData.Estatus"
            class="p-2 rounded-lg w-full bg-gray-100 border border-gray-300 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
            required
          >
            <option :value="null" disabled>Estatus de la Rutina</option>
            <option value="Activo">Activo</option>
            <option value="Inactivo">Inactivo</option>
          </select>
          <input
            v-model="formData.Resultados_Esperados"
            type="text"
            placeholder="Resultados Esperados"
            class="p-2 rounded-lg w-full bg-gray-100 border border-gray-300 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
          />
        </div>
        <button
          type="submit"
          class="px-4 py-2 rounded bg-red-600 text-white hover:bg-red-700 focus:outline-none transition-colors"
        >
          {{ isEditing ? "Actualizar Rutina" : "Crear Rutina" }}
        </button>
        <button
          type="button"
          @click="resetForm"
          class="ml-4 px-4 py-2 rounded bg-gray-400 text-white hover:bg-gray-500 focus:outline-none transition-colors"
        >
          Cancelar
        </button>
      </form>
      <div v-if="errorMessage" class="text-red-600 mt-4">{{ errorMessage }}</div>
    </section>

    <!-- Sección de la Tabla -->
    <section v-if="!showForm" class="table-responsive">
      <table class="w-full bg-white text-left text-sm text-gray-900 rounded shadow">
        <thead class="bg-gray-50 text-center">
          <tr>
            <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-l-md">Nombre</th>
            <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Programa Saludable ID</th>
            <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Tiempo Aproximado</th>
            <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Estatus</th>
            <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Resultados Esperados</th>
            <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-r-md">Acciones</th>
          </tr>
        </thead>
        <tbody class="bg-gray-200">
          <tr v-for="(rutina, i) in rutinas" :key="rutina.ID" class="hover:bg-gray-300">
            <td class="h-[50px] text-center">{{ rutina.Nombre }}</td>
            <td class="text-center">{{ rutina.Programa_Saludable_ID }}</td>
            <td class="text-center">{{ rutina.Tiempo_Aproximado }}</td>
            <td class="text-center">{{ rutina.Estatus }}</td>
            <td class="text-center">{{ rutina.Resultados_Esperados }}</td>
            <td class="flex justify-center space-x-2">
              <button @click="editRutina(rutina)" class="px-4 py-2 rounded-md bg-blue-600 text-white hover:bg-blue-700 focus:outline-none transition-colors flex items-center">Editar</button>
              <button @click="deleteRutina(rutina.ID)" class="px-4 py-2 rounded-md bg-red-600 text-white hover:bg-red-700 focus:outline-none transition-colors flex items-center">Eliminar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </section>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      showForm: false,
      isEditing: false,
      formData: {
        Nombre: '',
        Programa_Saludable_ID: 0,
        Fecha_Registro: new Date().toISOString(),
        Fecha_Actualizacion: new Date().toISOString(),
        Tiempo_Aproximado: '',
        Estatus: '',
        Resultados_Esperados: ''
      },
      rutinas: [],
      errorMessage: '',
      editingID: null,
    };
  },
  methods: {
    toggleForm() {
      this.showForm = !this.showForm;
      if (!this.showForm) {
        this.resetForm();
      }
    },
    async submitForm() {
      try {
        if (this.isEditing) {
          await axios.put(
            `https://gimnasio-deploy.onrender.com/rutinas`,
            this.formData, 
            {
              headers: {
                'Content-Type': 'application/json',
                'Authorization': `Bearer ${localStorage.getItem('token')}`,
              },
            }
          );
        } else {
          const response = await axios.post('https://gimnasio-deploy.onrender.com/rutinas',this.formData, {
            headers: {
              'Content-Type': 'application/json',
              'Authorization': `Bearer ${localStorage.getItem('token')}`,
            },
          });
          this.rutinas.push(response.data);
        }
        this.resetForm();
        this.toggleForm(); // Oculta el formulario después de guardar
        this.fetchRutinas(); // Refresca la lista de rutinas
      } catch (error) {
        console.error(error);
        this.errorMessage = 'Hubo un error al enviar los datos. Inténtalo de nuevo.';
      }
    },
    resetForm() {
      this.formData = {
        Nombre: '',
        Programa_Saludable_ID: 0,
        Fecha_Registro: new Date().toISOString(),
        Fecha_Actualizacion: new Date().toISOString(),
        Tiempo_Aproximado: '',
        Estatus: '',
        Resultados_Esperados: ''
      };
      this.isEditing = false;
      this.errorMessage = '';
      this.editingID = null;
    },
    async fetchRutinas() {
      try {
        const response = await axios.get('https://gimnasio-deploy.onrender.com/rutinas', {
          headers: {
            'Authorization': `Bearer ${localStorage.getItem('token')}`,
          },
        });
        this.rutinas = response.data;
      } catch (error) {
        console.error(error);
        this.errorMessage = 'No se pudo cargar la lista de rutinas.';
      }
    },
    async deleteRutina(id) {
      try {
        await axios.delete(`https://gimnasio-deploy.onrender.com/rutina/${id}`, {
          headers: {
            'Authorization': `Bearer ${localStorage.getItem('token')}`,
          },
        });
        this.rutinas = this.rutinas.filter(rutina => rutina.ID !== id);
      } catch (error) {
        console.error(error);
        this.errorMessage = 'No se pudo eliminar la rutina. Inténtalo de nuevo.';
      }
    },
    editRutina(rutina) {
      this.formData = { ...rutina };
      this.isEditing = true;
      this.editingID = rutina.ID;
      this.showForm = true;
    }
  },
  mounted() {
    this.fetchRutinas(); // Carga la lista de rutinas al montar el componente
  },
};
</script>

<style scoped>
/* Estilos adicionales aquí */
</style>
