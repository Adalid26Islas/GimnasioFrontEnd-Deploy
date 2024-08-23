<template>
  <div>
    <h1 class="title-gym">BULL'S GYM</h1>
    <main class="w-[100%] h-auto ml-2">
      <section>
        <div class="mx-auto p-4">
          <div class="bg-gray-900 dark:bg-gray-700 shadow rounded-lg p-6">
            <h1 class="text-xl font-semibold mb-4 text-gray-100 dark:text-gray-100">Agregar Productos</h1>
            <p class="text-gray-100 dark:text-gray-100 mb-6">
              Ingresa la información correspondiente para crear un nuevo producto.
            </p>
            <form @submit.prevent="agregarProducto">
              <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                <input v-model="nuevoProducto.nombre" type="text" placeholder="Nombre de Producto"
                       class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                <input v-model="nuevoProducto.marca" type="text" placeholder="Marca"
                       class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                <input v-model="nuevoProducto.precio" type="number" placeholder="Precio Actual"
                       class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
              </div>
              <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                <input v-model="nuevoProducto.codigoBarras" type="text" placeholder="Código de barras"
                       class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                <input v-model="nuevoProducto.descripcion" type="text" placeholder="Descripción"
                       class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                <input v-model="nuevoProducto.presentacion" type="text" placeholder="Presentación"
                       class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
              </div>
              <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                <select v-model="nuevoProducto.estatus"
                  class="rounded-lg w-full font-medium bg-gray-100 border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                  <option value="">Estatus</option>
                  <option value="activo">Activo</option>
                  <option value="inactivo">Inactivo</option>
                </select>
                <div class="relative mt-5">
                  <input
                    v-model="nuevoProducto.fechaRegistro"
                    id="fecha-registro"
                    class="w-full px-8 py-4 rounded-lg font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
                    type="date"
                    required
                  />
                  <label for="fecha-registro" class="absolute left-3 top-0 -translate-y-1/2 transform bg-white px-1 text-gray-500 text-xs">
                    Fecha de registro
                  </label>
                </div>
                <div class="relative mt-5">
                  <input
                    v-model="nuevoProducto.fechaActualizacion"
                    id="fecha-actualizacion"
                    type="date"
                    class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white"
                    required
                  />
                  <label for="fecha-actualizacion" class="absolute left-3 top-0 -translate-y-1/2 transform bg-white px-1 text-gray-500 text-xs">
                    Fecha de actualización
                  </label>
                </div>
              </div>
              <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                <input type="file" @change="handleFileChange" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
              </div>
              <button type="submit" class="px-1 py-1 w-[30%] rounded bg-red-600 text-white hover:bg-gray-600 focus:outline-none transition-colors">
                Agregar Producto
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
              <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Nombre de Producto</th>
              <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Marca</th>
              <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Precio</th>
              <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Fecha de Creación</th>
              <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Fecha de Actualización</th>
              <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100"></th>
              <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-r-md"></th>
            </tr>
          </thead>
          <tbody class="bg-gray-200">
            <tr v-for="producto in productos" :key="producto.ID" class="hover:bg-gray-500">
              <td class="h-[50px] text-center"><span>{{ producto.ID }}</span></td>
              <td class="h-[50px] text-center"><span>{{ producto.nombre }}</span></td>
              <td class="h-[50px] text-center"><span>{{ producto.marca }}</span></td>
              <td class="text-center"><span>{{ producto.precio }}</span></td>
              <td class="text-center"><span>{{ producto.fechaRegistro }}</span></td>
              <td class="text-center"><span>{{ producto.fechaActualizacion }}</span></td>
              <td class="text-center">
                <button @click="editarProducto(producto)" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                  Editar Producto
                </button>
              </td>
              <td class="text-center">
                <button @click="eliminarProducto(producto)" class="px-4 mt-1 py-2 rounded-md bg-gray-900 text-white hover:bg-gray-600">
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
      nuevoProducto: {
        nombre: '',
        marca: '',
        precio: null,
        codigoBarras: '',
        descripcion: '',
        presentacion: '',
        estatus: '',
        fechaRegistro: '',
        fechaActualizacion: '',
        fotografia: null
      },
      productos: [],
    };
  },
  methods: {
    async agregarProducto() {
      try {
        const formData = new FormData();

        // Mapear los nombres de las propiedades si es necesario
        formData.append('Nombre', this.nuevoProducto.nombre);
        formData.append('Marca', this.nuevoProducto.marca);
        formData.append('Cod_barras', this.nuevoProducto.codigoBarras);
        formData.append('Descripcion', this.nuevoProducto.descripcion);
        formData.append('Presentacion', this.nuevoProducto.presentacion);
        formData.append('Precio_actual', parseInt(this.nuevoProducto.precio)); // Convertir a entero
        formData.append('Estatus', this.nuevoProducto.estatus === 'activo' ? 1 : 0); // Convertir a TINYINT
        formData.append('Fecha_registro', this.nuevoProducto.fechaRegistro);
        formData.append('Fecha_actualizacion', this.nuevoProducto.fechaActualizacion);

        if (this.nuevoProducto.fotografia) {
          formData.append('Fotografia', this.nuevoProducto.fotografia.name); // Enviar solo el nombre del archivo
        }

        const response = await axios.post('http://127.0.0.1:8000/productos', formData, {
          headers: {
            'Content-Type': 'multipart/form-data',
            'Authorization': `Bearer ${localStorage.getItem('token')}`
          }
        });

        this.productos.push(response.data);
        this.resetForm();
      } catch (error) {
        console.error("Error al agregar producto:", error.response ? error.response.data : error.message);
      }
    },
    // Otros métodos que tienes, como editarProducto, eliminarProducto, etc.
    async editarProducto(producto) {
      this.nuevoProducto = { ...producto };
    },
    async eliminarProducto(producto) {
      try {
        await axios.delete(`http://127.0.0.1:8000/productos/${producto.ID}`, {
          headers: {
            'Authorization': `Bearer ${localStorage.getItem('token')}`
          }
        });
        this.productos = this.productos.filter(p => p.ID !== producto.ID);
      } catch (error) {
        console.error("Error al eliminar producto:", error);
      }
    },
    handleFileChange(event) {
      const file = event.target.files[0];
      if (file) {
        this.nuevoProducto.fotografia = file;
      }
    },
    resetForm() {
      this.nuevoProducto = {
        nombre: '',
        marca: '',
        precio: null,
        codigoBarras: '',
        descripcion: '',
        presentacion: '',
        estatus: '',
        fechaRegistro: '',
        fechaActualizacion: '',
        fotografia: null
      };
    },
    async fetchProductos() {
      try {
        const response = await axios.get('http://127.0.0.1:8000/productos', {
          headers: {
            'Authorization': `Bearer ${localStorage.getItem('token')}`
          }
        });
        this.productos = response.data;
      } catch (error) {
        console.error("Error al obtener productos:", error);
      }
    }
  },
  created() {
    this.fetchProductos();
  }
};
</script>

<style scoped>
/* Tus estilos aquí */
</style>