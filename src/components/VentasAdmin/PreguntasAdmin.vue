<template>
  <div>
    <h1 class="text-2xl xl:text-3xl font-extrabold mb-6">Preguntas de Clientes</h1>

    <!-- Formulario para añadir una nueva pregunta -->
    <form @submit.prevent="addQuestion">
      <input
        v-model="newQuestion.Pregunta"
        class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
        type="text" placeholder="Pregunta" required
      />
      <input
        v-model="newQuestion.Respuesta"
        class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
        type="text" placeholder="Respuesta" required
      />
      <input
        v-model="newQuestion.Categoria"
        class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
        type="text" placeholder="Categoría" required
      />
      <input
        v-model="newQuestion.Persona"
        class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
        type="text" placeholder="Persona" required
      />
      <select v-model="newQuestion.Estatus"
        class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
        required>
        <option value="" disabled hidden>Estatus</option>
        <option value="Cancelada">Cancelada</option>
        <option value="Registrada">Registrada</option>
        <option value="Pendiente">Pendiente</option>
        <option value="Atendida">Atendida</option>
      </select>
      <div class="relative mt-5">
        <input
          v-model="newQuestion.FechaCreacion"
          id="fecha-creacion"
          class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
          type="date"
          required
        />
        <label for="fecha-creacion" class="absolute left-3 top-0 -translate-y-1/2 transform bg-white px-1 text-gray-500 text-xs">
          Fecha Creación
        </label>
      </div>
      <div class="relative mt-5">
        <input
          v-model="newQuestion.FechaActualizacion"
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
        class="mt-5 tracking-wide font-semibold bg-red-700 text-red-100 w-full py-4 rounded-lg hover:bg-red-900 transition-all duration-300 ease-in-out flex items-center justify-center focus:shadow-outline focus:outline-none"
        type="submit"
      >
        Registrar
      </button>
    </form>

    <!-- Listado de preguntas -->
    <h2 class="text-xl font-bold mt-10">Lista de Preguntas de Clientes</h2>
    <table class="min-w-full bg-white mt-5">
      <thead>
        <tr>
          <th class="py-2">ID</th>
          <th class="py-2">Pregunta</th>
          <th class="py-2">Respuesta</th>
          <th class="py-2">Categoría</th>
          <th class="py-2">Persona</th>
          <th class="py-2">Estatus</th>
          <th class="py-2">Fecha Creación</th>
          <th class="py-2">Fecha Actualización</th>
          <th class="py-2">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="question in questions" :key="question.id">
          <td class="border px-4 py-2">{{ question.id }}</td>
          <td class="border px-4 py-2">{{ question.Pregunta }}</td>
          <td class="border px-4 py-2">{{ question.Respuesta }}</td>
          <td class="border px-4 py-2">{{ question.Categoria }}</td>
          <td class="border px-4 py-2">{{ question.Persona }}</td>
          <td class="border px-4 py-2">{{ question.Estatus }}</td>
          <td class="border px-4 py-2">{{ question.FechaCreacion }}</td>
          <td class="border px-4 py-2">{{ question.FechaActualizacion }}</td>
          <td class="border px-4 py-2 text-center">
            <div class="flex justify-center gap-2">
              <button @click="editQuestion(question.id)" class="bg-yellow-500 text-white px-4 py-2 rounded-lg w-24">
                Editar
              </button>
              <button @click="deleteQuestion(question.id)" class="bg-red-500 text-white px-4 py-2 rounded-lg w-24">
                Eliminar
              </button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>

    <!-- Formulario para editar una pregunta -->
    <div v-if="editingQuestion">
      <h2 class="text-xl font-bold mt-10">Editar Pregunta</h2>
      <form @submit.prevent="updateQuestion">
        <input
          v-model="currentQuestion.Pregunta"
          class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
          type="text" placeholder="Pregunta" required
        />
        <input
          v-model="currentQuestion.Respuesta"
          class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
          type="text" placeholder="Respuesta" required
        />
        <input
          v-model="currentQuestion.Categoria"
          class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
          type="text" placeholder="Categoría" required
        />
        <input
          v-model="currentQuestion.Persona"
          class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
          type="text" placeholder="Persona" required
        />
        <select v-model="currentQuestion.Estatus"
          class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white mt-5"
          required>
          <option value="" disabled hidden>Estatus</option>
          <option value="Cancelada">Cancelada</option>
          <option value="Registrada">Registrada</option>
          <option value="Pendiente">Pendiente</option>
          <option value="Atendida">Atendida</option>
        </select>
        <div class="relative mt-5">
          <input
            v-model="currentQuestion.FechaCreacion"
            id="fecha-creacion"
            class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
            type="date"
            required
          />
          <label for="fecha-creacion" class="absolute left-3 top-0 -translate-y-1/2 transform bg-white px-1 text-gray-500 text-xs">
            Fecha Creación
          </label>
        </div>
        <div class="relative mt-5">
          <input
            v-model="currentQuestion.FechaActualizacion"
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
          class="mt-5 tracking-wide font-semibold bg-blue-700 text-blue-100 w-full py-4 rounded-lg hover:bg-blue-900 transition-all duration-300 ease-in-out flex items-center justify-center focus:shadow-outline focus:outline-none"
          type="submit"
        >
          Actualizar
        </button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      questions: [],
      newQuestion: {
        Pregunta: '',
        Respuesta: '',
        Categoria: '',
        Persona: '',
        Estatus: '',
        FechaCreacion: '',
        FechaActualizacion: ''
      },
      editingQuestion: false,
      currentQuestion: {}
    };
  },
  methods: {
    async fetchQuestions() {
      try {
        const response = await axios.get('http://127.0.0.1:8000/Pregunta');
        this.questions = response.data;
      } catch (error) {
        console.error('Error fetching questions:', error);
      }
    },
    async addQuestion() {
      try {
        const response = await axios.post('http://127.0.0.1:8000/Pregunta', this.newQuestion);
        this.questions.push(response.data);
        this.newQuestion = {
          Pregunta: '',
          Respuesta: '',
          Categoria: '',
          Persona: '',
          Estatus: '',
          FechaCreacion: '',
          FechaActualizacion: ''
        };
      } catch (error) {
        console.error('Error adding question:', error);
      }
    },
    async editQuestion(id) {
      try {
        const response = await axios.get(`http://127.0.0.1:8000/Pregunta/${id}`);
        this.currentQuestion = response.data;
        this.editingQuestion = true;
      } catch (error) {
        console.error('Error fetching question for editing:', error);
      }
    },
    async updateQuestion() {
      try {
        const response = await axios.put(`http://127.0.0.1:8000/Pregunta/${this.currentQuestion.id}`, this.currentQuestion);
        const index = this.questions.findIndex(q => q.id === this.currentQuestion.id);
        if (index !== -1) {
          this.questions[index] = response.data;
        }
        this.editingQuestion = false;
        this.currentQuestion = {};
      } catch (error) {
        console.error('Error updating question:', error);
      }
    },
    async deleteQuestion(id) {
      try {
        await axios.delete(`http://127.0.0.1:8000/Pregunta/${id}`);
        this.questions = this.questions.filter(question => question.id !== id);
      } catch (error) {
        console.error('Error deleting question:', error);
      }
    }
  },
  created() {
    this.fetchQuestions();
  }
};
</script>

<style scoped>
/* Añade estilos específicos si es necesario */
</style>