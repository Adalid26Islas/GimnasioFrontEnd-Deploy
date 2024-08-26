<template>
    <h1 class="title-gym">BULL'S GYM</h1>
    <main class="w-[100%] h-auto ml-2">
        <section>
            <div class="mx-auto p-4">
                <div class="bg-white-900 white:bg-white-700 shadow rounded-lg p-6">
                    <h1 class="text-xl font-semibold mb-4 text-dark-100 dark:text-dark-100">Crear nueva membresía</h1>
                    <p class="text-dark-100 dark:text-dark-100 mb-6">Ingresa la información correspondiente para crear
                        una nueva membresía.</p>
                    <form>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            <input type="text" v-model="this.membresiaData.Codigo" placeholder="Código"
                                class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                            <select v-model="this.membresiaData.Tipo"
                                class="rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                                <option value="">Tipo</option>
                                <option value="Individual">Individual</option>
                                <option value="Familiar">Familiar</option>
                                <option value="Empresarial">Empresarial</option>
                            </select>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            <select v-model="this.membresiaData.Tipo_Servicios"
                                class="rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                                <option value="">Tipo de servicios</option>
                                <option value="Basicos">Básicos</option>
                                <option value="Completa">Completa</option>
                                <option value="Coaching">Coaching</option>
                                <option value="Nutrilogo">Nutriólogo</option>
                            </select>
                            <select v-model="this.membresiaData.Tipo_Plan"
                                class="rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                                <option value="">Tipo de plan</option>
                                <option value="Anual">Anual</option>
                                <option value="Semestral">Semestral</option>
                                <option value="Trimestral">Trimestral</option>
                                <option value="Bimestral">Bimestral</option>
                                <option value="Mensual">Mensual</option>
                                <option value="Semanal">Semanal</option>
                                <option value="Diaria">Diaria</option>
                            </select>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            <select v-model="this.membresiaData.Nivel"
                                class="rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                                <option value="">Nivel</option>
                                <option value="Nuevo">Nuevo</option>
                                <option value="Plata">Plata</option>
                                <option value="Oro">Oro</option>
                                <option value="Diamante">Diamante</option>
                            </select>
                            <input id="fecha_inicio" type="date" v-model="this.membresiaData.Fecha_Inicio" placeholder="Fecha de Inicio"
                                class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            <input type="date" v-model="this.membresiaData.Fecha_Fin" placeholder="Fecha de Fin"
                                class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                            <select v-model="this.membresiaData.Estatus"
                                class="rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                                <option value="">Estatus</option>
                                <option value="true">Activo</option>
                                <option value="false">Inactivo</option>
                            </select>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            <input type="date" v-model="this.membresiaData.Fecha_Registro" placeholder="Fecha de Registro"
                                class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                        </div>
                        <button type="button" @click="submitForm" id="membresia"
                            class="px-4 py-2 w-[20%] rounded bg-red-600 text-white hover:bg-gray-600 focus:outline-none transition-colors">
                            Crear membresía
                        </button>
                    </form>
                </div>
            </div>
            <hr class="border-2 m-4 mt-1">
        </section>
        <section class="mx-auto p-4">
            <!-- Botón de acción con menú desplegable -->
            <div
                class="flex items-center justify-between flex-column flex-wrap md:flex-row space-y-4 md:space-y-0 pb-4 bg-white dark:bg-gray-900">
                <div>
                    <button id="dropdownActionButton" data-dropdown-toggle="dropdownAction"
                        class="inline-flex items-center text-gray-500 bg-white border border-gray-300 focus:outline-none hover:bg-gray-100 focus:ring-4 focus:ring-gray-100 font-medium rounded-lg text-sm px-3 py-1.5 dark:bg-gray-800 dark:text-gray-400 dark:border-gray-600 dark:hover:bg-gray-700 dark:hover:border-gray-600 dark:focus:ring-gray-700"
                        type="button">
                        <span class="sr-only">Action button</span>
                        Actions
                        <svg class="w-2.5 h-2.5 ms-2.5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg"
                            fill="none" viewBox="0 0 10 6">
                            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="m1 1 4 4 4-4" />
                        </svg>
                    </button>
                    <!-- Dropdown menu -->
                    <div id="dropdownAction"
                        class="z-10 hidden bg-white divide-y divide-gray-100 rounded-lg shadow w-44 dark:bg-gray-700 dark:divide-gray-600">
                        <ul class="py-1 text-sm text-gray-700 dark:text-gray-200"
                            aria-labelledby="dropdownActionButton">
                            <li>
                                <a href="#"
                                    class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white">Eliminar</a>
                            </li>
                            <li>
                                <a href="#"
                                    class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white">Ordenar
                                    A-Z</a>
                            </li>
                            <li>
                                <a href="#"
                                    class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white">Ordenar
                                    Z-A</a>
                            </li>
                        </ul>
                    </div>
                </div>
                <!-- Campo de búsqueda -->
                <label for="table-search" class="sr-only">Search</label>
                <div class="relative">
                    <div class="absolute inset-y-0 rtl:inset-r-0 start-0 flex items-center ps-3 pointer-events-none">
                        <svg class="w-4 h-4 text-gray-500 dark:text-gray-400" aria-hidden="true"
                            xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
                            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z" />
                        </svg>
                    </div>
                    <input type="text" id="table-search-users"
                        class="block p-2 ps-10 text-sm text-gray-900 border border-gray-300 rounded-lg w-80 bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                        placeholder="Buscar por código">
                </div>
            </div>
            <hr class="border-2 mt-4">
        </section>
        <section class="m-4">
            <table class="w-full bg-white text-left text-sm text-gray-900 rounded">
                <thead class="bg-gray-50 text-center">
                    <tr>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-l-md">ID</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Código</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Tipo</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Tipo de Servicios</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Tipo de Plan</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Nivel</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Fecha de Inicio</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Fecha de Fin</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Estatus</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-r-md">Acciones
                        </th>
                    </tr>
                </thead>
                <tbody class="bg-white divide-y divide-gray-200">
                    <tr>
                        <td class="px-6 py-4 text-center font-medium text-gray-900">1</td>
                        <td class="px-6 py-4 text-center text-gray-700">MEMB001</td>
                        <td class="px-6 py-4 text-center text-gray-700">Regular</td>
                        <td class="px-6 py-4 text-center text-gray-700">Entrenamiento</td>
                        <td class="px-6 py-4 text-center text-gray-700">Básico</td>
                        <td class="px-6 py-4 text-center text-gray-700">Avanzado</td>
                        <td class="px-6 py-4 text-center text-gray-700">2024-01-01</td>
                        <td class="px-6 py-4 text-center text-gray-700">2024-12-31</td>
                        <td class="px-6 py-4 text-center text-gray-700">Activo</td>
                        <td class="px-6 py-4 text-center text-gray-700">
                            <button class="text-blue-600 hover:underline">Editar</button>
                            <button class="text-red-600 hover:underline">Eliminar</button>
                        </td>
                    </tr>
                    <!-- Más filas aquí -->
                </tbody>
            </table>
        </section>
    </main>
</template>
<script>
export default {
    data() {
        return {
            membresiaData: {
                Codigo: "string",
                Tipo: "string",
                Tipo_Servicios: "string",
                Tipo_Plan: "string",
                Nivel: "string",
                Fecha_Inicio: "2024-08-20T16:55:28.908Z",
                Fecha_Fin: "2024-08-20T16:55:28.908Z",
                Estatus: true,
                Fecha_Registro: "2024-08-20T16:55:28.908Z",
                Fecha_Actualizacion: (new Date(Date.now())).toISOString()
            }
        }
    },
    methods: {
        async submitForm() {
            this.membresiaData.Estatus = this.membresiaData.Estatus === 'true' ? true : false;
            console.log(JSON.stringify(this.membresiaData))
            const url = "https://gimnasio-deploy.onrender.com/membresia/"
            const token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJOb21icmVfVXN1YXJpbyI6IkFsZGFpciIsIkNvcnJlb19FbGVjdHJvbmljbyI6InN0cmluZyIsIkNvbnRyYXNlbmEiOiIxMjMiLCJOdW1lcm9fVGVsZWZvbmljb19Nb3ZpbCI6InN0cmluZyJ9.5EsBwNW9FIyMzd3jqJOA-vvdhvFrMvNL2bWhfnliFKQ"
            await fetch(url, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Bearer ${token}`
                },
                body: JSON.stringify(this.membresiaData)
            })
                .then(response => {
                    if (!response.ok) {
                        throw new Error('Error en la solicitud: ' + response.statusText);
                    }
                    return response.json();
                })
                .then(data => {
                    console.log('Respuesta de la API:', data);
                })
                .catch(error => {
                    console.error('Error:', error);
                });
        }
    }
}
</script>