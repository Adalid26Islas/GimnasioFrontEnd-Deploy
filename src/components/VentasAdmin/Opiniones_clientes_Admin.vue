<template>
  <div>
    <h1 class="text-2xl xl:text-3xl font-extrabold mb-6">Opiniones Clientes</h1>

    <!-- Formulario para añadir un nuevo programa -->
    <form @submit.prevent="addProgram">
      <input
        v-model="newProgram.Descripcion"
        class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
        type="text" placeholder="Descripcion" required
      />
      <input
        v-model="newProgram.id_usuario"
        class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
        type="text" placeholder="ID Usuario" required
      />
      <input
        v-model="newProgram.Tipo"
        class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
        type="text" placeholder="Tipo" required
      />
      <input
        v-model="newProgram.Respuesta"
        class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
        type="text" placeholder="Respuesta" required
      />
      <select v-model="newProgram.Estatus"
    class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"> 
        <option value="" disabled selected hidden>Estatus</option>
        <option value="Cancelado">Cancelado</option>
        <option value="Registrado">Registrado</option>
        <option value="Abierto">Abierto</option>
        <option value="Atendida">Atendida</option>
      </select>

      <div class="relative mt-5">
  <input
    v-model="newProgram.Registro"
    id="fecha-registro"
    class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
    type="date"
    required
  />
  <label for="fecha-registro" class="absolute left-3 top-0 -translate-y-1/2 transform bg-white px-1 text-gray-500 text-xs">
    Fecha Registro
  </label>
</div>

<div class="relative mt-5">
  <input
    v-model="newProgram.Actualizacion"
    id="fecha-actualizacion"
    class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
    type="date"
    required
  />
  <label for="fecha-actualizacion" class="absolute left-3 top-0 -translate-y-1/2 transform bg-white px-1 text-gray-500 text-xs">
    Fecha Actualización
  </label>
</div>

      <input
        v-model="newProgram.Atencion"
        class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
        type="text" placeholder="Atencion Personal" required
      />
      <button
        class="mt-5 tracking-wide font-semibold bg-red-700 text-red-100 w-full py-4 rounded-lg hover:bg-red-900 transition-all duration-300 ease-in-out flex items-center justify-center focus:shadow-outline focus:outline-none col-span-2"
        type="submit"
      >
        Registrar
      </button>
    </form>

    <!-- Listado de programas -->
    <h2 class="text-xl font-bold mt-10">Lista de Opiniones Clientes</h2>
    <table class="min-w-full bg-white mt-5">
      <thead>
        <tr>
          <th class="py-2">ID</th>
          <th class="py-2">ID usuario</th>
          <th class="py-2">Descripcion</th>
          <th class="py-2">Tipo</th>
          <th class="py-2">Respuesta</th>
          <th class="py-2">Estatus</th>
          <th class="py-2">Atencion Personal</th>
          <th class="py-2">Fecha Registro</th>
          <th class="py-2">Fecha Actualizacion</th>
          <th class="py-2">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="program in programs" :key="program.id">
          <td class="border px-4 py-2">{{ program.id }}</td>
          <td class="border px-4 py-2">{{ program.id_usuario }}</td>
          <td class="border px-4 py-2">{{ program.Descripcion }}</td>
          <td class="border px-4 py-2">{{ program.Tipo }}</td>
          <td class="border px-4 py-2">{{ program.Respuesta }}</td>
          <td class="border px-4 py-2">{{ program.Estatus }}</td>
          <td class="border px-4 py-2">{{ program.Atencion }}</td>
          <td class="border px-4 py-2">{{ program.Registro }}</td>
          <td class="border px-4 py-2">{{ program.Actualizacion }}</td>
          <td class="border px-4 py-2">
            <button @click="editProgram(program.id)" class="bg-yellow-500 text-white px-4 py-2 rounded">
              Editar
            </button>
            <button @click="deleteProgram(program.id)" class="bg-red-500 text-white px-4 py-2 rounded ml-2">
              Eliminar
            </button>
          </td>
        </tr>
      </tbody>
    </table>

    <!-- Formulario para editar un programa -->
    <div v-if="editingProgram">
      <h2 class="text-xl font-bold mt-10">Editar Opinion</h2>
      <form @submit.prevent="updateProgram">
        <input
          v-model="currentProgram.Descripcion"
          class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
          type="text" placeholder="Descripcion" required
        />
        <input
          v-model="currentProgram.Tipo"
          class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
          type="text" placeholder="Tipo" required
        />
        <input
          v-model="currentProgram.Respuesta"
          class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
          type="text" placeholder="Respuesta" required
        />
        <select v-model="currentProgram.Estatus"
           class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5">
            <option selected>Estatus</option>
            <option value="Cancelado">Cancelado</option>
            <option value="Regsitrado">Regsitrado</option>
            <option value="Abierto">Abierto</option>
            <option value="Atendida">Atendida</option>
        </select>
        <input
          v-model="currentProgram.Atencion"
          class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
          type="text" placeholder="Atencion Personal" required
        />
        <div class="relative mt-5">
  <input
    v-model="currentProgram.Registro"
    id="fecha-registro"
    class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
    type="date"
    required
  />
  <label for="fecha-registro" class="absolute left-3 top-0 -translate-y-1/2 transform bg-white px-1 text-gray-500 text-xs">
    Fecha Registro
  </label>
</div>

<div class="relative mt-5">
  <input
    v-model="currentProgram.Actualizacion"
    id="fecha-actualizacion"
    class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
    type="date"
    required
  />
  <label for="fecha-actualizacion" class="absolute left-3 top-0 -translate-y-1/2 transform bg-white px-1 text-gray-500 text-xs">
    Fecha Actualización
  </label>
</div>
        <button
          class="mt-5 tracking-wide font-semibold bg-blue-700 text-gray-100 w-full py-4 rounded-lg hover:bg-blue-900 transition-all duration-300 ease-in-out flex items-center justify-center focus:shadow-outline focus:outline-none col-span-2"
          type="submit"
        >
          Actualizar
        </button>
        <br>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      programs: [],
      newProgram: {
        Descripcion: "",
        Tipo: "",
        Respuesta: "",
        Estatus: "",
        Registro: "",
        Actualizacion: "",
        Atencion: ""
      },
      currentProgram: null,
      editingProgram: false
    };
  },
  methods: {
    async fetchPrograms() {
      try {
        const response = await axios.get('http://127.0.0.1:8000/OpinionCliente');
        this.programs = response.data;
      } catch (error) {
        console.error('Error fetching programs:', error);
      }
    },
    async addProgram() {
      try {
        const response = await axios.post('http://127.0.0.1:8000/OpinionCliente', this.newProgram);
        this.programs.push(response.data);
        this.newProgram = { Descripcion: "", Tipo: "", Respuesta: "", Estatus: "", Registro: "", Actualizacion: "", Atencion: "" };
      } catch (error) {
        console.error('Error adding program:', error);
      }
    },
    async editProgram(id) {
      try {
        const response = await axios.get(`http://127.0.0.1:8000/OpinionCliente${id}`);
        this.currentProgram = response.data;
        this.editingProgram = true;
      } catch (error) {
        console.error('Error fetching program for editing:', error);
      }
    },
    async updateProgram() {
      try {
        const response = await axios.put(`http://127.0.0.1:8000/OpinionCliente${this.currentProgram.id}`, this.currentProgram);
        const index = this.programs.findIndex(p => p.id === this.currentProgram.id);
        if (index !== -1) {
          this.programs.splice(index, 1, response.data);
        }
        this.currentProgram = null;
        this.editingProgram = false;
      } catch (error) {
        console.error('Error updating program:', error);
      }
    },
    async deleteProgram(id) {
      try {
        await axios.delete(`http://127.0.0.1:8000/OpinionCliente/${id}`);
        this.programs = this.programs.filter(p => p.id !== id);
      } catch (error) {
        console.error('Error deleting program:', error);
      }
    }
  },
  created() {
    this.fetchPrograms();
  }
};
</script>

