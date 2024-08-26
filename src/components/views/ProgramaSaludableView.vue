<template>
  <div class="mx-auto p-4">
    <h1 class="title-gym">BULL'S GYM</h1>
    <!-- Botón para mostrar el formulario -->
    <button
      v-if="!showForm"
      @click="toggleForm"
      class="px-4 py-2 mb-4 rounded bg-blue-600 text-white hover:bg-blue-700 focus:outline-none transition-colors"
    >
      Crear Programa Saludable
    </button>

    <!-- Sección del Formulario -->
    <section v-if="showForm" class="mb-8 p-4 bg-white rounded shadow">
      <h1 class="text-xl font-semibold mb-4 text-gray-900">
        {{ isEditing ? "Actualizar Programa Saludable" : "Crear nuevo Programa Saludable" }}
      </h1>
      <p class="text-gray-700 mb-6">
        {{
          isEditing
            ? "Actualiza la información del programa seleccionado."
            : "Ingresa la información correspondiente para crear un nuevo programa."
        }}
      </p>

      <form @submit.prevent="submitForm">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
          <input
            v-model="formData.Nombre"
            type="text"
            placeholder="Nombre del Programa"
            class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
            required
          />
          <input
            v-model="formData.Usuario_ID"
            type="text"
            placeholder="ID del Usuario"
            class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
            required
          />
          <input
            v-model="formData.Instructor_ID"
            type="text"
            placeholder="ID del Instructor"
            class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
            required
          />
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
          <input
            v-model="formData.Fecha_Creacion"
            type="date"
            placeholder="Fecha de Creación"
            class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
            required
          />
          <select
            v-model="formData.Estatus"
            class="rounded-lg w-full font-medium bg-gray-100 border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
            required
            placeholder="Estatus"
          >
            <option :value="null">Selecciona el Estatus</option>
            <option v-for="status in statusOptions" :key="status" :value="status">{{ status }}</option>
          </select>
          <input
            v-model="formData.Duracion"
            type="text"
            placeholder="Duración"
            class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
            required
          />
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
          <input
            v-model="formData.Porcentaje_Avance"
            type="number"
            placeholder="Porcentaje de Avance"
            class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
            step="0.01"
            required
          />
          <input
            v-model="formData.Fecha_Ultima_Actualizacion"
            type="date"
            placeholder="Fecha de Última Actualización"
            class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
            required
          />
        </div>
        <button
          type="submit"
          class="px-4 py-2 rounded bg-red-600 text-white hover:bg-red-700 focus:outline-none transition-colors"
        >
          {{ isEditing ? "Actualizar Programa" : "Crear Programa" }}
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
    <section class="m-4">
      <table class="w-full bg-white text-left text-sm text-gray-900 rounded">
        <thead class="bg-gray-50 text-center">
          <tr>
            <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">ID</th>
            <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">NOMBRE</th>
            <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">USUARIO</th>
            <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">INSTRUCTOR</th>
            <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">FECHA CREACIÓN</th>
            <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">ESTATUS</th>
            <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">DURACIÓN</th>
            <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">PORCENTAJE AVANCE</th>
            <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">FECHA ÚLTIMA ACTUALIZACIÓN</th>
            <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100 rounded-r-md">ACCIONES</th>
          </tr>
        </thead>
        <tbody class="bg-gray-200">
          <tr v-for="(programa, i) in programas" :key="programa.ID" class="hover:bg-gray-300">
            <td class="h-[50px] text-center">{{ programa.ID }}</td>
            <td class="text-center">{{ programa.Nombre }}</td>
            <td class="text-center">{{ programa.Usuario_ID }}</td>
            <td class="text-center">{{ programa.Instructor_ID }}</td>
            <td class="text-center">{{ new Date(programa.Fecha_Creacion).toLocaleDateString() }}</td>
            <td class="text-center">{{ programa.Estatus }}</td>
            <td class="text-center">{{ programa.Duracion }}</td>
            <td class="text-center">{{ programa.Porcentaje_Avance }}%</td>
            <td class="text-center">{{ new Date(programa.Fecha_Ultima_Actualizacion).toLocaleDateString() }}</td>
            <td class="flex justify-center space-x-2">
              <button @click="editPrograma(programa)" class="px-4 py-2 rounded-md bg-blue-600 text-white hover:bg-blue-700 focus:outline-none transition-colors flex items-center">
                Editar
              </button>
              <button @click="deletePrograma(programa.ID)" class="px-4 py-2 rounded-md bg-red-600 text-white hover:bg-red-700 focus:outline-none transition-colors flex items-center">
                Eliminar
              </button>
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
        Usuario_ID: '',
        Instructor_ID: '',
        Fecha_Creacion: new Date().toISOString().split('T')[0],
        Estatus: '',
        Duracion: '',
        Porcentaje_Avance: '',
        Fecha_Ultima_Actualizacion: new Date().toISOString().split('T')[0]
      },
      programas: [],
      errorMessage: '',
      editingID: null,
      statusOptions: [
        'Registrado', 'Sugerido', 'Iniciado', 'En Proceso', 'Finalizado'
      ]
    };
  },
  methods: {
    toggleForm() {
      this.showForm = !this.showForm;
      if (!this.showForm) {
        this.resetForm();
      }
    },
    resetForm() {
      this.isEditing = false;
      this.editingID = null;
      this.formData = {
        Nombre: '',
        Usuario_ID: '',
        Instructor_ID: '',
        Fecha_Creacion: new Date().toISOString().split('T')[0],
        Estatus: '',
        Duracion: '',
        Porcentaje_Avance: '',
        Fecha_Ultima_Actualizacion: new Date().toISOString().split('T')[0]
      };
      this.showForm = false;
      this.errorMessage = '';
    },
    async submitForm() {
      try {
        if (this.isEditing && this.editingID) {
          const response = await axios.put(`https://api.example.com/programas_saludables/${this.editingID}`, this.formData);
          this.programas = this.programas.map((programa) =>
            programa.ID === this.editingID ? response.data : programa
          );
        } else {
          const response = await axios.post('https://api.example.com/programas_saludables/', this.formData);
          this.programas.push(response.data);
        }
        this.resetForm();
        this.fetchProgramas();
      } catch (error) {
        console.error('Error al enviar el formulario:', error);
        this.errorMessage = 'Hubo un error al enviar el formulario. Por favor, intente de nuevo.';
      }
    },
    async fetchProgramas() {
      try {
        const response = await axios.get('https://api.example.com/programas_saludables/');
        this.programas = response.data;
      } catch (error) {
        console.error('Error al obtener programas:', error);
        this.errorMessage = 'Hubo un error al obtener los programas. Por favor, intente de nuevo.';
      }
    },
    editPrograma(programa) {
      this.isEditing = true;
      this.showForm = true;
      this.editingID = programa.ID;
      this.formData = { ...programa };
    },
    async deletePrograma(programaID) {
      try {
        await axios.delete(`https://api.example.com/programas_saludables/${programaID}`);
        this.programas = this.programas.filter((programa) => programa.ID !== programaID);
      } catch (error) {
        console.error('Error al eliminar el programa:', error);
        this.errorMessage = 'Hubo un error al eliminar el programa. Por favor, intente de nuevo.';
      }
    }
  },
  mounted() {
    this.fetchProgramas();
  }
};
</script>

<style scoped>
.title-gym {
  font-size: 28px;
  font-weight: bold;
  text-align: center;
  color: #1a202c;
  margin-bottom: 20px;
}
</style>
