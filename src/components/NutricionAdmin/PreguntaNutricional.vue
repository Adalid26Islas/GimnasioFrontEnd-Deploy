<template>
    <label for="" class="block mt-3 text-xl text-gray-700 text-center font-extrabold">
        Adeudo
    </label>
   
    <form ref="formAdeudo">

        <div class="grid gap-12 mb-12 sm:grid-cols-2 mt-8 ">
            <div>
                <label class="px-1 block text-sm uppercase text-gray-500 mb-2 font-extrabold">Area</label>
                <input type="text" v-model="formAdeudo.Area" name="Area" id="Area"
                    class="font-bold hover:bg-blue-100 focus:bg-blue-100 rounded-sm shadow-sm  focus:ring-0 w-full px-3 py-2 mb-5 border border-gray-300 rounded-xl placeholder-gray-400"
                    placeholder="Nombre">

            </div>
            <div>
                <label class="px-1 block text-sm uppercase text-gray-500 mb-2 font-extrabold">Cliente</label>
                <input type="text" v-model="formAdeudo.Cliente" name="Cliente" id="Cliente"
                    class="font-bold hover:bg-blue-100 focus:bg-blue-100 rounded-sm shadow-sm  focus:ring-0 w-full px-3 py-2 mb-5 border border-gray-300 rounded-xl placeholder-gray-400"
                    placeholder="Direccion ">
            </div>
            <div>
                <label class="px-1 block text-sm uppercase text-gray-500 mb-2 font-extrabold">Descripcion
                </label>
                <input type="text" v-model="formAdeudo.Descripcion" name="Descripcion" id="Descripcion"
                    class="font-bold hover:bg-blue-100 focus:bg-blue-100 rounded-sm shadow-sm  focus:ring-0 w-full px-3 py-2 mb-5 border border-gray-300 rounded-xl placeholder-gray-400"
                    placeholder="Responsable">
            </div>
            <div>
                <label class="px-1 block text-sm uppercase text-gray-500 mb-2 font-extrabold">Tipo
                </label>
                <input type="text" v-model="formAdeudo.Tipo" name="Tipo" id="Tipo"
                    class="font-bold hover:bg-blue-100 focus:bg-blue-100 rounded-sm shadow-sm  focus:ring-0 w-full px-3 py-2 mb-5 border border-gray-300 rounded-xl placeholder-gray-400"
                    placeholder="Total clientes atendidos">
            </div>
            <div>
                <label class="px-1 block text-sm uppercase text-gray-500 mb-2 font-extrabold">Detalle</label>
                <select v-model="formAdeudo.Detalle" name="Detalle" id="Detalle"
                        class="font-bold hover:bg-blue-100 focus:bg-blue-100 rounded-sm shadow-sm  focus:ring-0 w-full px-3 py-2 mb-5 border border-gray-300 rounded-xl placeholder-gray-400">
                        <option value="">-- Selecciona detalle --</option>
                        <option value="Producto">Producto</option>
                        <option value="Equipamiento">Equipamiento</option>
                        <option value="Servicio">Servicior</option>
                    </select>
            </div>
            <div>

            </div>

            <a type="submit"
                class="w-full bg-blue-600 hover:bg-blue-700 text-white font-extrabold py-3 cursor-pointer transition duration-500 ease-in-out  transform hover:-translate-x hover:scale-105 rounded-xl text-center"
                @click="extractFormAdeudo">Enviar</a>

        </div>
    </form>
    <!-- Tabla para mostrar los datos -->
    <div class="mt-8">
            <table class="min-w-full divide-y divide-gray-200">
                <thead class="bg-gray-50">
                    <tr>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Area</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Cliente</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Descripcion</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Tipo</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Detalle</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Fecha Registro</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Fecha Actualización</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Estatus</th>
                    </tr>
                </thead>
                <tbody class="bg-white divide-y divide-gray-200">
                    <tr v-for="adeudo in adeudos" :key="adeudo.id">
                        <td class="px-6 py-4 whitespace-nowrap">{{ adeudo.Area }}</td>
                        <td class="px-6 py-4 whitespace-nowrap">{{ adeudo.Cliente }}</td>
                        <td class="px-6 py-4 whitespace-nowrap">{{ adeudo.Descripcion }}</td>
                        <td class="px-6 py-4 whitespace-nowrap">{{ adeudo.Tipo }}</td>
                        <td class="px-6 py-4 whitespace-nowrap">{{ adeudo.Detalle }}</td>
                        <td class="px-6 py-4 whitespace-nowrap">{{ adeudo.Fecha_Registro }}</td>
                        <td class="px-6 py-4 whitespace-nowrap">{{ adeudo.Fecha_Actualizacion }}</td>
                        <td class="px-6 py-4 whitespace-nowrap">{{ adeudo.Estatus ? 'Activo' : 'Inactivo' }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            formAdeudo: {
                Area: '',
                Cliente: '',
                Descripcion: '',
                Tipo: '',
                Detalle: '',
            },
            adeudos: []  // Agregado para almacenar los datos de los adeudos
        }
    },

    methods: {
        extractFormAdeudo() {
            const AdeudosInformacion = {
                Area: this.formAdeudo.Area,
                Cliente: this.formAdeudo.Cliente,
                Descripcion: this.formAdeudo.Descripcion,
                Fecha_Registro: new Date().toISOString(),
                Fecha_Actualizacion: new Date().toISOString(),
                Estatus: true,
                Tipo: this.formAdeudo.Tipo,
                Detalle: this.formAdeudo.Detalle,
            };
            console.log(AdeudosInformacion);

            const url = "http://127.0.0.1:8000/adeudo/"
            const token = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJOb21icmVfVXN1YXJpbyI6InZhbGVuY2lhIiwiQ29ycmVvX0VsZWN0cm9uaWNvIjoic3RyaW5nIiwiQ29udHJhc2VuYSI6InF3ZXJ0eSIsIk51bWVyb19UZWxlZm9uaWNvX01vdmlsIjoic3RyaW5nIn0.Uh_BqQ80nlptFtbN-H38hOx_C0uvDCPidwuF_nj18is'

            axios
                .post(url, AdeudosInformacion, { headers: { Authorization: Bearer ${token} } })
                .then((response) => {
                    console.log("Datos enviados a la base", response.data);
                    this.fetchAdeudos();  // Actualiza la tabla después de enviar
                })
                .catch((error) => { console.error(error) });
        },

        fetchAdeudos() {
            const url = "http://127.0.0.1:8000/adeudo/"
            const token = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJOb21icmVfVXN1YXJpbyI6InZhbGVuY2lhIiwiQ29ycmVvX0VsZWN0cm9uaWNvIjoic3RyaW5nIiwiQ29udHJhc2VuYSI6InF3ZXJ0eSIsIk51bWVyb19UZWxlZm9uaWNvX01vdmlsIjoic3RyaW5nIn0.Uh_BqQ80nlptFtbN-H38hOx_C0uvDCPidwuF_nj18is'

            axios
                .get(url, { headers: { Authorization: Bearer ${token} } })
                .then((response) => {
                    this.adeudos = response.data;
                })
                .catch((error) => { console.error(error) });
        }
    },

    mounted() {
        this.fetchAdeudos();  // Llama a fetchAdeudos cuando el componente se monta para cargar los datos iniciales
    }
}
</script>