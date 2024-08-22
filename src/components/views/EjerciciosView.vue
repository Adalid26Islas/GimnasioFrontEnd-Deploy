<template>
  <div class="container mx-auto p-4">
    <div class="mb-4 flex justify-center space-x-4">
      <button @click="mostrarFormulario = !mostrarFormulario" class="px-4 py-2 rounded bg-red-600 text-white hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-red-500 transition-colors">
        {{ mostrarFormulario ? 'Ocultar' : 'Registrar' }} Ejercicio
      </button>
    </div>
    
    <div v-if="mostrarFormulario" class="flex flex-col gap-4">
      <form @submit.prevent="registrarEjercicio" class="bg-gray-400 p-4 shadow">
        <!-- Location Section -->
        <div class="md:flex mb-8">
          <div class="md:w-1/3">
            <legend class="uppercase tracking-wide text-sm">Ejercicio</legend>
            <p class="text-xs font-light text-red">Este campo es obligatorio.</p>
          </div>
          <div class="md:flex-1 mt-2 mb:mt-0 md:px-3">
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Nombre</label>
              <input v-model="nombre" class="w-full shadow-inner p-4 border-0" type="text" id="nombre" required placeholder="Nombre del ejercicio" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Descripción</label>
              <textarea v-model="descripcion" class="w-full shadow-inner p-4 border-0" id="descripcion" required placeholder="Descripción del ejercicio" rows="4"></textarea>
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Video</label>
              <input @change="handleFileUpload" class="w-full shadow-inner p-4 border-0" type="file" id="video" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Tipo</label>
              <input v-model="tipo" class="w-full shadow-inner p-4 border-0" type="text" id="tipo" required placeholder="Tipo de ejercicio" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Estatus</label>
              <input v-model="estatus" class="w-full shadow-inner p-4 border-0" type="text" id="estatus" required placeholder="Estatus del ejercicio" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Dificultad</label>
              <input v-model="dificultad" class="w-full shadow-inner p-4 border-0" type="text" id="dificultad" required placeholder="Dificultad del ejercicio" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Fecha Registro</label>
              <input v-model="fechaRegistro" class="w-full shadow-inner p-4 border-0" type="date" id="fechaRegistro" required />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Fecha Actualización</label>
              <input v-model="fechaActualizacion" class="w-full shadow-inner p-4 border-0" type="date" id="fechaActualizacion" required />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Recomendaciones</label>
              <textarea v-model="recomendaciones" class="w-full shadow-inner p-4 border-0" id="recomendaciones" required placeholder="Recomendaciones del ejercicio" rows="4"></textarea>
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Restricciones</label>
              <textarea v-model="restricciones" class="w-full shadow-inner p-4 border-0" id="restricciones" required placeholder="Restricciones del ejercicio" rows="4"></textarea>
            </div>
            <div class="md:flex mb-6 border border-t-1 border-b-0 border-x-0 border-cream-dark">
              <div class="md:flex-1 px-3 text-center md:text-right">
                <button type="submit" class="button text-cream-lighter bg-brick hover:bg-brick-dark">
                  Registrar Ejercicio
                </button>
              </div>
            </div>
          </div>
        </div>
      </form>
    </div>
    
    <TableEjercicios :ejercicio="ejercicios" />
  </div>
</template>

<script>
import TableEjercicios from '../TableEjercicios.vue';

export default {
  components: {
    TableEjercicios,
  },
  data() {
    return {
      mostrarFormulario: false,
      nombre: '',
      descripcion: '',
      video: null,
      tipo: '',
      estatus: '',
      dificultad: '',
      fechaRegistro: '',
      fechaActualizacion: '',
      recomendaciones: '',
      restricciones: '',
      ejercicios: [],  
    };
  },
  methods: {
    handleFileUpload(event) {
      this.video = event.target.files[0];
    },
    async registrarEjercicio() {
      const formData = new FormData();
      formData.append('Nombre', this.nombre);
      formData.append('Descripcion', this.descripcion);
      formData.append('Video', this.video);
      formData.append('Tipo', this.tipo);
      formData.append('Estatus', this.estatus);
      formData.append('Dificultad', this.dificultad);
      formData.append('Fecha_Registro', this.fechaRegistro);
      formData.append('Fecha_Actualizacion', this.fechaActualizacion);
      formData.append('Recomendaciones', this.recomendaciones);
      formData.append('Restricciones', this.restricciones);

      try {
        const response = await fetch('http://localhost:8000/ejercicios', {
          method: 'POST',
          body: formData,
        });

        if (!response.ok) {
          const error = await response.json();
          alert(error.detail);
        } else {
          const nuevoEjercicio = await response.json();
          this.ejercicios.push(nuevoEjercicio);  
          this.limpiarFormulario(); 
        }
      } catch (error) {
        console.error('Error al registrar ejercicio:', error);
      }
    },
    limpiarFormulario() {
      this.nombre = '';
      this.descripcion = '';
      this.video = null;
      this.tipo = '';
      this.estatus = '';
      this.dificultad = '';
      this.fechaRegistro = '';
      this.fechaActualizacion = '';
      this.recomendaciones = '';
      this.restricciones = '';
      this.mostrarFormulario = false;
    },
  },
};
</script>

<style scoped>
/* Asegúrate de incluir estos estilos en tu archivo CSS o directamente en el bloque de estilos */
body {
  background-color: #4a4a4a;
  color: #333;
  font-family: 'Sans-serif';
  overflow-x: hidden;
}

button {
  background-color: #b71c1c; /* Color rojo oscuro */
  color: #ffffff; /* Color blanco para el texto */
}

button:hover {
  background-color: #c62828; /* Rojo más oscuro en hover */
}

input, textarea {
  background-color: #f5f5f5;
  border: none;
  padding: 0.5rem;
  box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
  border-radius: 0.25rem;
}

button[type="submit"] {
  background-color: #c62828; /* Color de fondo del botón */
  color: #ffffff; /* Color del texto del botón */
  border-radius: 0.25rem;
  padding: 0.75rem 1.5rem;
}

button[type="submit"]:hover {
  background-color: #b71c1c; /* Color más oscuro en hover */
}
</style>
