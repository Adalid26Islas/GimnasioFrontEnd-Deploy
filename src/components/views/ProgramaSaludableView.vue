<template>
  <div>
    <h1 class="text-2xl xl:text-3xl font-extrabold mb-6 text-gray-100 dark:text-gray-100">Programas Saludables</h1>

    <!-- Formulario para añadir un nuevo programa -->
    <form @submit.prevent="addProgram">
      <input
        v-model="newProgram.name"
        class="w-full px-4 py-2 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mb-4"
        type="text" placeholder="Nombre del Programa Saludable" required
      />
      <input
        v-model="newProgram.status"
        class="w-full px-4 py-2 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mb-4"
        type="text" placeholder="Estatus" required
      />
      <input
        v-model="newProgram.duration"
        class="w-full px-4 py-2 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mb-4"
        type="text" placeholder="Duración" required
      />
      <input
        v-model="newProgram.progress"
        class="w-full px-4 py-2 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mb-4"
        type="number" placeholder="Porcentaje de Avance" required
      />
      <button
        class="w-full px-4 py-2 rounded bg-red-600 text-white hover:bg-red-700 focus:outline-none transition-colors mb-6"
        type="submit"
      >
        Registrar
      </button>
    </form>

    <!-- Listado de programas -->
    <h2 class="text-xl font-bold mt-10 text-gray-100 dark:text-gray-100">Lista de Programas Saludables</h2>
    <table class="w-full bg-white text-left text-sm text-gray-900 rounded mt-4">
      <thead class="bg-gray-900 text-gray-100">
        <tr>
          <th class="px-6 py-4">ID</th>
          <th class="px-6 py-4">Nombre</th>
          <th class="px-6 py-4">Estatus</th>
          <th class="px-6 py-4">Duración</th>
          <th class="px-6 py-4">Porcentaje de Avance</th>
          <th class="px-6 py-4">Acciones</th>
        </tr>
      </thead>
      <tbody class="bg-gray-200">
        <tr v-for="program in programs" :key="program.id" class="hover:bg-gray-300">
          <td class="px-4 py-2">{{ program.id }}</td>
          <td class="px-4 py-2">{{ program.name }}</td>
          <td class="px-4 py-2">{{ program.status }}</td>
          <td class="px-4 py-2">{{ program.duration }}</td>
          <td class="px-4 py-2">{{ program.progress }}%</td>
          <td class="px-4 py-2">
            <button @click="editProgram(program.id)" class="bg-yellow-500 text-white px-4 py-2 rounded">
              Editar
            </button>
            <button @click="deleteProgram(program.id)" class="bg-red-600 text-white px-4 py-2 rounded ml-2">
              Eliminar
            </button>
          </td>
        </tr>
      </tbody>
    </table>

    <!-- Formulario para editar un programa -->
    <div v-if="editingProgram" class="mt-10">
      <h2 class="text-xl font-bold text-gray-100 dark:text-gray-100">Editar Programa</h2>
      <form @submit.prevent="updateProgram">
        <input
          v-model="currentProgram.name"
          class="w-full px-4 py-2 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mb-4"
          type="text" placeholder="Nombre del Programa Saludable" required
        />
        <input
          v-model="currentProgram.status"
          class="w-full px-4 py-2 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mb-4"
          type="text" placeholder="Estatus" required
        />
        <input
          v-model="currentProgram.duration"
          class="w-full px-4 py-2 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mb-4"
          type="text" placeholder="Duración" required
        />
        <input
          v-model="currentProgram.progress"
          class="w-full px-4 py-2 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mb-4"
          type="number" placeholder="Porcentaje de Avance" required
        />
        <button
          class="w-full px-4 py-2 rounded bg-blue-700 text-gray-100 hover:bg-blue-800 focus:outline-none transition-colors"
          type="submit"
        >
          Actualizar
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      programs: [
        { id: 1, name: "Programa de Nutrición", status: "Activo", duration: "3 meses", progress: 75 },
        { id: 2, name: "Entrenamiento Funcional", status: "Inactivo", duration: "6 meses", progress: 40 },
        { id: 3, name: "Yoga Avanzado", status: "Activo", duration: "1 mes", progress: 100 }
      ],
      newProgram: {
        name: "",
        status: "",
        duration: "",
        progress: 0
      },
      currentProgram: null,
      editingProgram: false
    };
  },
  methods: {
    addProgram() {
      if (this.newProgram.name && this.newProgram.status && this.newProgram.duration && this.newProgram.progress) {
        const newId = this.programs.length + 1;
        this.programs.push({ ...this.newProgram, id: newId });
        this.newProgram = { name: "", status: "", duration: "", progress: 0 };
      }
    },
    editProgram(id) {
      this.currentProgram = { ...this.programs.find(p => p.id === id) };
      this.editingProgram = true;
    },
    updateProgram() {
      const index = this.programs.findIndex(p => p.id === this.currentProgram.id);
      if (index !== -1) {
        this.programs.splice(index, 1, this.currentProgram);
      }
      this.currentProgram = null;
      this.editingProgram = false;
    },
    deleteProgram(id) {
      this.programs = this.programs.filter(p => p.id !== id);
    }
  }
};
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}
th, td {
  border: 1px solid #ddd;
  text-align: left;
  padding: 8px;
}
</style>
