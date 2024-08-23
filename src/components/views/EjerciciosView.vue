<template>
  <div class="mx-auto p-4">
    <!-- Botón para agregar nuevo Ejercicio -->
    <section class="mb-4">
      <button @click="toggleForm" class="px-4 py-2 rounded bg-red-600 text-white hover:bg-red-700 focus:outline-none transition-colors">
        {{ showForm ? 'Cerrar Formulario' : 'Agregar Nuevo Ejercicio' }}
      </button>
    </section>

    <div class="bg-gray-900 dark:bg-gray-700 shadow rounded-lg p-6">
      <!-- Formulario para agregar nuevo Ejercicio (se muestra/oculta al hacer clic en el botón) -->
      <h1 class="text-xl font-semibold mb-4 text-gray-900">{{ isEditing ? 'Editar Ejercicio' : 'Crear nuevo Ejercicio' }}</h1>
      <section v-if="showForm" class="mb-8 p-4 dark:bg-gray-700 rounded shadow">
        <form @submit.prevent="submitForm">
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
            <input 
              v-model="formData.Nombre" 
              type="text" 
              placeholder="Nombre del Ejercicio" 
              class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-300 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" 
              required>
            <textarea 
              v-model="formData.Descripcion" 
              placeholder="Descripción del Ejercicio" 
              class="p-2 rounded-lg font-medium bg-gray-100 border border-gray-300 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" 
              required></textarea>
            <select 
              v-model="formData.Tipo" 
              class="rounded-lg w-full font-medium bg-gray-100 border border-gray-300 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" 
              required>
              <option value="" disabled>Selecciona Tipo</option>
              <option value="Aerobico">Aeróbico</option>
              <option value="Resistencia">Resistencia</option>
              <option value="Flexibilidad">Flexibilidad</option>
              <option value="Fuerza">Fuerza</option>
            </select>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold text-gray-900">Video</label>
              <input @change="handleFileUpload" type="text" class="w-full p-2 rounded-lg bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" id="video" />

            </div>
          </div>
          <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
            <select 
              v-model="formData.Estatus" 
              class="rounded-lg w-full font-medium bg-gray-100 border border-gray-300 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" 
              required>
              <option value="" disabled>Estatus</option>
              <option value="false">Inactivo</option>
              <option value="true">Activo</option>
            </select>
            <select 
              v-model="formData.Dificultad" 
              class="rounded-lg w-full font-medium bg-gray-100 border border-gray-300 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" 
              required>
              <option value="" disabled>Selecciona Dificultad</option>
              <option value="Facil">Fácil</option>
              <option value="Intermedio">Intermedio</option>
              <option value="Dificil">Difícil</option>
            </select>
          </div>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
            <textarea 
              v-model="formData.Recomendaciones" 
              placeholder="Recomendaciones del Ejercicio" 
              class="w-full p-2 rounded-lg font-medium bg-gray-100 border border-gray-300 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" 
              required></textarea>
            <textarea 
              v-model="formData.Restricciones" 
              placeholder="Restricciones del Ejercicio" 
              class="w-full p-2 rounded-lg font-medium bg-gray-100 border border-gray-300 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white" 
              required></textarea>
          </div>
          <button type="submit" class="px-4 py-2 rounded bg-red-600 text-white hover:bg-red-700 focus:outline-none transition-colors">
            {{ isEditing ? 'Actualizar Ejercicio' : 'Crear Ejercicio' }}
          </button>
        </form>
        <div v-if="errorMessage" class="text-red-600 mt-4">{{ errorMessage }}</div>
      </section>

      <!-- Sección de la Tabla -->
      <section class="m-4">
        <table class="w-full bg-white text-left text-sm text-gray-900 rounded">
          <thead class="bg-gray-50 text-center">
            <tr>
              <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100 rounded-r-md">ID</th>
              <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">NOMBRE</th>
              <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">DESCRIPCIÓN</th>
              <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">TIPO</th>
              <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">ESTATUS</th>
              <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">DIFICULTAD</th>
              <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">FECHA REGISTRO</th>
              <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100">FECHA ACTUALIZACIÓN</th>
              <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100 rounded-r-md">VIDEO</th>
              <th scope="col" class="px-6 py-4 bg-red-900 font-medium text-gray-100 rounded-r-md">ACCIONES</th>
            </tr>
          </thead>
          <tbody class="bg-gray-200">
            <tr v-for="(ejercicio, i) in ejercicios" :key="ejercicio.ID" class="hover:bg-gray-300">
              <td class="h-[50px] text-center">{{ ejercicio.ID }}</td>
              <td class="text-center">{{ ejercicio.Nombre }}</td>
              <td class="text-center">{{ ejercicio.Descripcion }}</td>
              <td class="text-center">{{ ejercicio.Tipo }}</td>
              <td class="text-center">{{ ejercicio.Estatus ? 'Activo' : 'Inactivo' }}</td>
              <td class="text-center">{{ ejercicio.Dificultad }}</td>
              <td class="text-center">{{ new Date(ejercicio.Fecha_Registro).toLocaleDateString() }}</td>
              <td class="text-center">{{ new Date(ejercicio.Fecha_Actualizacion).toLocaleDateString() }}</td>
              <td class="text-center">
                <a v-if="ejercicio.Video" :href="ejercicio.Video" target="_blank" class="text-blue-500 underline">Ver Video</a>
                <span v-else>No disponible</span>
              </td>
              <td class="flex justify-center space-x-2">
                <button @click="editEjercicio(ejercicio)" class="px-4 py-2 rounded-md bg-blue-600 text-white hover:bg-blue-700 focus:outline-none transition-colors flex items-center">
                  Editar
                </button>
                <button @click="deleteEjercicio(ejercicio.ID, ejercicio.Nombre)" class="px-4 py-2 rounded-md bg-red-600 text-white hover:bg-red-700 focus:outline-none transition-colors flex items-center">
                  Eliminar
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </section>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      showForm: false, // Controla la visibilidad del formulario
      isEditing: false, // Indica si estamos en modo de edición
      formData: {
        ID: null,
        Nombre: '',
        Tipo: '',
        Descripcion: '',
        Estatus: false,
        Dificultad: '',
        Recomendaciones: '',
        Restricciones: '',
        Fecha_Registro: new Date().toISOString(),
        Fecha_Actualizacion: new Date().toISOString(),
        Video: '' // Campo para la URL del video
      },
      ejercicios: [], // Lista de ejercicios
      errorMessage: '' // Mensaje de error
    };
  },
  methods: {
    toggleForm() {
      this.showForm = !this.showForm;
      if (this.showForm) {
        this.isEditing = false; // No estamos editando cuando mostramos el formulario
        this.resetForm();
      }
    },
    resetForm() {
      this.formData = {
        ID: null,
        Nombre: '',
        Tipo: '',
        Descripcion: '',
        Estatus: false,
        Dificultad: '',
        Recomendaciones: '',
        Restricciones: '',
        Fecha_Registro: new Date().toISOString(),
        Fecha_Actualizacion: new Date().toISOString(),
        Video: ''
      };
      this.errorMessage = '';
    },
    submitForm() {
      if (this.isEditing) {
        // Llamada para actualizar el ejercicio
        axios.put(`https://gimnasio-deploy.onrender.com/ejercicios`, this.formData, {
          headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${localStorage.getItem('token')}`
          },
        })
        .then(response => {
          this.fetchEjercicios(); // Refrescar la lista de ejercicios
          this.toggleForm();
        })
        .catch(error => {
          this.errorMessage = 'Error al actualizar el ejercicio. Inténtalo de nuevo.';
        });
      } else {
        // Llamada para crear un nuevo ejercicio
        axios.post('https://gimnasio-deploy.onrender.com/ejercicios', this.formData, {
          headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${localStorage.getItem('token')}`
          },
        })
        .then(response => {
          this.fetchEjercicios(); // Refrescar la lista de ejercicios
          this.toggleForm();
        })
        .catch(error => {
          this.errorMessage = 'Error al crear el ejercicio. Inténtalo de nuevo.';
        });
      }
    },
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (file) {
        if (!file.type.startsWith('video/')) {
          this.errorMessage = 'El archivo seleccionado no es un video.';
          return;
        }
        const formData = new FormData();
        formData.append('video', file);
        axios.post('https://gimnasio-deploy.onrender.com/ejercicio', formData, {
          headers: {
            'Content-Type': 'multipart/form-data',
            'Authorization': `Bearer ${localStorage.getItem('token')}`
          },
        })
        .then(response => {
          this.formData.Video = response.data.url; // Asume que la respuesta contiene la URL del video
        })
        .catch(error => {
          this.errorMessage = 'Error al subir el video. Inténtalo de nuevo.';
        });
      }
    },
    editEjercicio(ejercicio) {
      this.isEditing = true;
      this.formData = { ...ejercicio };
      this.showForm = true;
    },
    deleteEjercicio(id, nombre) {
      if (confirm(`¿Estás seguro de que deseas eliminar el ejercicio "${nombre}"?`)) {
        axios.delete(`https://gimnasio-deploy.onrender.com/ejercicio/${id}`, {
          headers: {
            'Authorization': `Bearer ${localStorage.getItem('token')}`
          },
        })
        .then(() => {
          this.fetchEjercicios(); // Refrescar la lista de ejercicios
        })
        .catch(error => {
          this.errorMessage = 'Error al eliminar el ejercicio. Inténtalo de nuevo.';
        });
      }
    },
    fetchEjercicios() {
      axios.get('https://gimnasio-deploy.onrender.com/ejercicios', {
        headers: {
          'Authorization': `Bearer ${localStorage.getItem('token')}`
        },
      })
      .then(response => {
        this.ejercicios = response.data;
      })
      .catch(error => {
        this.errorMessage = 'Error al cargar los ejercicios. Inténtalo de nuevo.';
      });
    }
  },
  mounted() {
    this.fetchEjercicios(); // Cargar los ejercicios al montar el componente
  }
};
</script>

<style scoped>
/* Aquí puedes agregar estilos adicionales para el componente */
</style>
