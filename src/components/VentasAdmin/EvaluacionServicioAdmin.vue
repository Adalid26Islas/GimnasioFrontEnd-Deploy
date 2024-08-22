<template>
    <div>
      <h1 class="title-gym">BULL'S GYM</h1>
      <main class="w-[100%] h-auto ml-2">
        <section>
          <div class="mx-auto p-4">
            <div class="bg-gray-900 dark:bg-gray-700 shadow rounded-lg p-6">
              <h1 class="text-xl font-semibold mb-4 text-gray-100 dark:text-gray-100">Gestionar Evaluaciones</h1>
              <p class="text-gray-100 dark:text-gray-100 mb-6">
                Ingresa la información correspondiente para crear o editar una evaluación de servicio.
              </p>
              <form @submit.prevent="crearOeditarEvaluacion">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                  <input v-model="form.id" type="number" placeholder="ID" 
                         class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                  <input v-model="form.usuarioId" type="text" placeholder="Nombre de Usuario"
                         class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                  <select v-model="form.servicios" 
                          class="rounded-lg w-full font-medium bg-gray-100 border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                    <option value="">Seleccionar Servicio</option>
                    <option value="Servicio de Nutrición">Servicio de Nutrición</option>
                    <option value="Horarios y Precios">Horarios y Precios</option>
                    <option value="Comunidad">Comunidad</option>
                    <option value="Programas de entrenamiento">Programas de entrenamiento</option>
                    <!-- Añadir más opciones según los servicios disponibles -->
                  </select>
                  <input v-model="form.calificacion" type="number" placeholder="Calificación"
                         class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                  
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                  <input v-model="form.criterio" type="text" placeholder="Criterio"
                         class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                         <select v-model="form.servicios" 
                          class="rounded-lg w-full font-medium bg-gray-100 border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                    <option value="">Estatus</option>
                    <option value="1">Activo  </option>
                    <option value="0">Inactivo</option>
                  </select>
                </div>
                <div class="relative mb-6">
  <input
    v-model="form.fechaRegistro"
    id="fecha-registro"
    type="date"
    class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
    required
  />
  <label for="fecha-registro" class="absolute left-3 top-0 -translate-y-1/2 transform bg-white px-1 text-gray-500 text-xs">
    Fecha de Registro
  </label>
</div>

                <button type="submit" class="px-4 py-2 w-[30%] rounded bg-red-600 text-white hover:bg-gray-600 focus:outline-none transition-colors">
                  {{ isEditing ? 'Actualizar Evaluación' : 'Crear Evaluación' }}
                </button>
              </form>
            </div>
          </div>
          <hr class="border-2 m-4 mt-1">
        </section>
        <section class="m-4">
          <table class="w-full bg-white text-left text-sm text-gray-900 rounded">
            <thead class="bg-gray-50 text-center">
              <tr>
                <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-l-md">ID</th>
                <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Nombre de Usuario</th>
                <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Servicio</th>
                <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Calificación</th>
                <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Criterio</th>
                <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Estatus</th>
                <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Fecha de Registro</th>
                <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-r-md"></th>
                <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-r-md"></th>
              </tr>
            </thead>
            <tbody class="bg-gray-200">
              <tr v-for="evaluacion in evaluaciones" :key="evaluacion.id" class="hover:bg-gray-500">
                <td class="text-center">{{ evaluacion.id }}</td>
                <td class="text-center">{{ evaluacion.usuarioId }}</td>
                <td class="text-center">{{ evaluacion.servicios }}</td>
                <td class="text-center">{{ evaluacion.calificacion }}</td>
                <td class="text-center">{{ evaluacion.criterio }}</td>
                <td class="text-center">{{ evaluacion.estatus }}</td>
                <td class="text-center">{{ evaluacion.fechaRegistro }}</td>
                <td class="text-center">
                  <button @click="editarEvaluacion(evaluacion)" class="px-4 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                    Editar
                  </button>
                </td>
                <td class="text-center">
                  <button @click="eliminarEvaluacion(evaluacion.id)" class="px-4 py-2 rounded-md bg-gray-900 text-white hover:bg-gray-600">
                    Eliminar
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
          <hr class="border-2 mt-4">
        </section>
      </main>
    </div>
  </template>
  
  <script>

  import axios from 'axios';

  export default {
  data() {
    return {
      form: {
        id: null,
        usuarioId: null,
        calificacion: '',
        criterio: '',
        servicios: '',
        estatus: '',
        fechaRegistro: ''
      },
      evaluaciones: [], // Inicia con una lista vacía
      isEditing: false
    };
  },
  methods: {
    async getEvaluaciones() {
      try {
        const response = await axios.get('https://gimnasio-deploy.onrender.com/docs/evaluaciones_serv', {
          headers: {
            'Authorization': `Bearer ${localStorage.getItem('token')}` // Token de autenticación si es necesario
          }
        });
        this.evaluaciones = response.data;
      } catch (error) {
        console.error('Error al cargar evaluaciones:', error);
      }
    },
    async crearOeditarEvaluacion() {
      if (this.isEditing) {
        // Lógica para actualizar evaluación
        try {
          await axios.put(`https://gimnasio-deploy.onrender.com/evaluaciones_serv/${this.form.id}`, this.form, {
            headers: {
              'Content-Type': 'application/json',
              'Authorization': `Bearer ${localStorage.getItem('token')}`
            }
          });
          const index = this.evaluaciones.findIndex(e => e.id === this.form.id);
          if (index !== -1) {
            this.$set(this.evaluaciones, index, { ...this.form });
          }
          this.isEditing = false;
        } catch (error) {
          console.error('Error al actualizar evaluación:', error);
        }
      } else {
        // Lógica para crear nueva evaluación
        try {
          const response = await axios.post('https://gimnasio-deploy.onrender.com/evaluaciones_serv', this.form, {
            headers: {
              'Content-Type': 'application/json',
              'Authorization': `Bearer ${localStorage.getItem('token')}`
            }
          });
          this.evaluaciones.push(response.data);
        } catch (error) {
          console.error('Error al crear evaluación:', error);
        }
      }
      // Limpiar formulario
      this.form = {
        id: null,
        usuarioId: null,
        calificacion: '',
        criterio: '',
        servicios: '',
        estatus: '',
        fechaRegistro: ''
      };
    },
    editarEvaluacion(evaluacion) {
      this.form = { ...evaluacion };
      this.isEditing = true;
    },
    async eliminarEvaluacion(id) {
      if (confirm('¿Estás seguro de que deseas eliminar esta evaluación?')) {
        try {
          await axios.delete(`https://gimnasio-deploy.onrender.com/evaluaciones_serv/${id}`, {
            headers: {
              'Authorization': `Bearer ${localStorage.getItem('token')}`
            }
          });
          this.evaluaciones = this.evaluaciones.filter(e => e.id !== id);
        } catch (error) {
          console.error('Error al eliminar evaluación:', error);
        }
      }
    }
  },
  mounted() {
    this.getEvaluaciones(); // Cargar las evaluaciones al montar el componente
  }
};
</script>
  <style scoped>
  /* Estilos personalizados */
  </style>
  