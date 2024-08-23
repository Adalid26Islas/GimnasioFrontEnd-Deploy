<template>
  
  <div class="bg-gray-700 text-charcoal font-sans leading-normal overflow-x-hidden lg:overflow-auto">
    <div class="grid sm:grid-cols-2 items-start gap-16 p-4 mx-auto max-w-4xl bg-white">
      <div>
        <h1 class="text-gray-800 text-3xl font-extrabold">Registro de Instructores</h1>
        <p class="text-sm text-gray-500 mt-4">Complete el formulario para registrar un nuevo instructor en el sistema.</p>

        <div class="mt-8">
          <img src="https://c8.alamy.com/comp/DRRP55/young-fitness-instructor-gym-people-spinning-DRRP55.jpg" alt="Imagen del Instructor"
            class="w-full h-auto rounded-lg shadow-md" />
        </div>
      </div>

      <Stepper :steps="['Datos Básicos', 'Experiencia y Contratación', 'Detalles del Instructor']" @submit="handleSubmit">
        <template v-slot="{ currentStep }">
          <div v-if="currentStep === 0">
            <!-- Datos Básicos -->
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Título de Cortesía</label>
              <input type="text" placeholder="Título de Cortesía"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Nombre</label>
              <input type="text" placeholder="Nombre"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Primer Apellido</label>
              <input type="text" placeholder="Primer Apellido"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Segundo Apellido</label>
              <input type="text" placeholder="Segundo Apellido"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Fecha de Nacimiento</label>
              <input type="date" placeholder="Fecha de Nacimiento"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Fotografía</label>
              <input type="file" placeholder="Fotografía"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Género</label>
              <select class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent">
                <option value="">Selecciona Género</option>
                <option value="Masculino">Masculino</option>
                <option value="Femenino">Femenino</option>
                <option value="Otro">Otro</option>
              </select>
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Tipo de Sangre</label>
              <select class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent">
                <option value="">Selecciona Tipo de Sangre</option>
                <option value="A+">A+</option>
                <option value="A-">A-</option>
                <option value="B+">B+</option>
                <option value="B-">B-</option>
                <option value="O+">O+</option>
                <option value="O-">O-</option>
                <option value="AB+">AB+</option>
                <option value="AB-">AB-</option>
              </select>
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Estatus</label>
              <select class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent">
                <option value="">Selecciona Estatus</option>
                <option value="Activo">Activo</option>
                <option value="Inactivo">Inactivo</option>
              </select>
            </div>
          </div>

          <div v-if="currentStep === 1">
            <!-- Experiencia y Contratación -->
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Área ID</label>
              <input type="number" placeholder="Área ID"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Fecha de Contratación</label>
              <input type="date" placeholder="Fecha de Contratación"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Puesto ID</label>
              <input type="text" placeholder="Puesto ID"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Número de Empleado</label>
              <input type="text" placeholder="Número de Empleado"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
          </div>

          <div v-if="currentStep === 2">
            <!-- Detalles del Instructor -->
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Persona ID</label>
              <input type="text" placeholder="Persona ID"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Email</label>
              <input type="email" placeholder="Email"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Teléfono</label>
              <input type="tel" placeholder="Teléfono"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Dirección</label>
              <input type="text" placeholder="Dirección"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <div class="mb-4">
              <label class="block uppercase tracking-wide text-xs font-bold">Observaciones</label>
              <textarea placeholder="Observaciones"
                class="w-full shadow-inner p-4 border-0 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent"></textarea>
            </div>
          </div>
        </template>

        <template v-slot:actions>
          <!-- Botones de Navegación ya están definidos en el componente Stepper -->
        </template>
      </Stepper>
    </div>
  </div>
</template>

<script>
import Stepper from '../Stepper.vue'; // Asegúrate de que la ruta sea correcta

export default {
  components: {
    Stepper
  },
  methods: {
    handleSubmit() {
      // Manejar el envío del formulario aquí
      console.log('Formulario enviado');
    }
  }
};
</script>

<style scoped>
/* Aquí puedes añadir estilos adicionales si es necesario */
</style>
