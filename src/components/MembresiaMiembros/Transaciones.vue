<template>
    <h1 class="title-gym">BULL'S GYM</h1>
    <main class="w-[100%] h-auto ml-2">
        <section>
            <div class="mx-auto p-4">
                <div class="bg-white-900 white:bg-white-700 shadow rounded-lg p-6">
                    <h1 class="text-xl font-semibold mb-4 text-dark-100 dark:text-dark-100">Crear nueva transacción</h1>
                    <p class="text-dark-100 dark:text-dark-100 mb-6">Ingresa la información correspondiente para crear una nueva transacción.</p>
                    <form>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            <input type="number" v-model="this.transaccionData.Usuario_ID" placeholder="Usuario ID" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                            <select v-model="this.transaccionData.Metodo_Pago" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                                <option value="">Método de Pago</option>
                                <option value="TarjetaCredito">Tarjeta de Crédito</option>
                                <option value="TarjetaDebito">Tarjeta de Débito</option>
                            </select>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            <input type="text" v-model="this.transaccionData.Numero_Tarjeta" placeholder="Número de Tarjeta" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                            <input type="number" v-model="this.transaccionData.CVC" placeholder="CVC" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            <input type="date" v-model="this.transaccionData.Fecha_Expiracion" placeholder="Fecha de Expiración" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                            <input type="number" v-model="this.transaccionData.Monto" placeholder="Monto" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            <select v-model="this.transaccionData.Estatus" class="rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                                <option value="">Estatus</option>
                                <option value="true">Activo</option>
                                <option value="false">Inactivo</option>
                            </select>
                            <input type="datetime-local" v-model="this.transaccionData.Fecha_Registro" placeholder="Fecha de Registro" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                        </div>
                        <button type="button" @click="submitForm" id="transaccion" class="px-4 py-2 w-[20%] rounded bg-red-600 text-white hover:bg-gray-600 focus:outline-none transition-colors">
                            Crear transacción
                        </button>
                    </form>
                </div>
            </div>
            <hr class="border-2 m-4 mt-1">
        </section>
        <section class="mx-auto p-4">
            <!-- Botón de acción con menú desplegable -->
            <div class="flex items-center justify-between flex-column flex-wrap md:flex-row space-y-4 md:space-y-0 pb-4 bg-white dark:bg-gray-900">
                <div>
                    <button id="dropdownActionButton" data-dropdown-toggle="dropdownAction" class="inline-flex items-center text-gray-500 bg-white border border-gray-300 focus:outline-none hover:bg-gray-100 focus:ring-4 focus:ring-gray-100 font-medium rounded-lg text-sm px-3 py-1.5 dark:bg-gray-800 dark:text-gray-400 dark:border-gray-600 dark:hover:bg-gray-700 dark:hover:border-gray-600 dark:focus:ring-gray-700" type="button">
                        <span class="sr-only">Action button</span>
                        Actions
                        <svg class="w-2.5 h-2.5 ms-2.5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
                            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m1 1 4 4 4-4"/>
                        </svg>
                    </button>
                    <!-- Dropdown menu -->
                    <div id="dropdownAction" class="z-10 hidden bg-white divide-y divide-gray-100 rounded-lg shadow w-44 dark:bg-gray-700 dark:divide-gray-600">
                        <ul class="py-1 text-sm text-gray-700 dark:text-gray-200" aria-labelledby="dropdownActionButton">
                            <li>
                                <a href="#" class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white">Eliminar</a>
                            </li>
                            <li>
                                <a href="#" class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white">Ordenar A-Z</a>
                            </li>
                            <li>
                                <a href="#" class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white">Ordenar Z-A</a>
                            </li>
                        </ul>
                    </div>
                </div>
                <!-- Campo de búsqueda -->
                <label for="table-search" class="sr-only">Search</label>
                <div class="relative">
                    <div class="absolute inset-y-0 rtl:inset-r-0 start-0 flex items-center ps-3 pointer-events-none">
                        <svg class="w-4 h-4 text-gray-500 dark:text-gray-400" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
                            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"/>
                        </svg>
                    </div>
                    <input type="text" id="table-search-users" class="block p-2 ps-10 text-sm text-gray-900 border border-gray-300 rounded-lg w-80 bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Buscar por usuario ID">
                </div>
            </div>
            <hr class="border-2 mt-4">
        </section>
        <section class="m-4">
            <table class="w-full bg-white text-left text-sm text-gray-900 rounded ">
                <thead class="bg-gray-50 text-center">
                    <tr>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-l-md">Usuario ID</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Método de Pago</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Número de Tarjeta</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">CVC</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Fecha de Expiración</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Monto</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Estatus</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Fecha de Registro</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-r-md">Fecha de Actualización</th>
                    </tr>
                </thead>
                <tbody class="text-center bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600"  v-for="transaccion in this.transaccionesTable" :key="transaccion.ID">
                    <!-- Filas de datos aquí -->
                    <tr >
                        <td class="px-6 py-4">{{ transaccion.Usuario_ID }}</td>
                        <td class="px-6 py-4">{{ transaccion.Metodo_Pago }}</td>
                        <td class="px-6 py-4">{{ transaccion.Numero_Tarjeta }}</td>
                        <td class="px-6 py-4">{{ transaccion.CVC }}</td>
                        <td class="px-6 py-4">{{ transaccion.Fecha_Expiracion }}</td>
                        <td class="px-6 py-4">{{ transaccion.Monto }}</td>
                        <td class="px-6 py-4">{{ transaccion.Estatus ? 'Activo' : 'Inactivo'}}</td>
                        <td class="px-6 py-4">{{ transaccion.Fecha_Registro }}</td>
                        <td class="px-6 py-4">{{ transaccion.Fecha_Actualizacion }}</td>
                    </tr>
                </tbody>
            </table>
        </section>
    </main>
</template>
<script>
export default {
    data() {
        return {
            transaccionData: {
                Usuario_ID: null,
                Metodo_Pago: null,
                Numero_Tarjeta: null,
                CVC: null,
                Fecha_Expiracion: null,
                Monto: null,
                Estatus: null,
                Fecha_Registro: null,
                Fecha_Actualizacion: (new Date(Date.now())).toISOString()
            },
            transaccionesTable:[]
        }
    },
    methods: {
        clearData() {
            this.transaccionData = {
                Usuario_ID: null,
                Metodo_Pago: null,
                Numero_Tarjeta: null,
                CVC: null,
                Fecha_Expiracion: null,
                Monto: null,
                Estatus: null,
                Fecha_Registro: null,
                Fecha_Actualizacion: (new Date(Date.now())).toISOString()
            }
        },
        async submitForm() {
            this.transaccionData.Estatus = this.transaccionData.Estatus === 'true' ? true : false;
            console.log(JSON.stringify(this.transaccionData))
            const url = "http://127.0.0.1:8000/transaccion/"
            const token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJOb21icmVfVXN1YXJpbyI6IkFsZGFpciIsIkNvcnJlb19FbGVjdHJvbmljbyI6InN0cmluZyIsIkNvbnRyYXNlbmEiOiIxMjMiLCJOdW1lcm9fVGVsZWZvbmljb19Nb3ZpbCI6InN0cmluZyJ9.5EsBwNW9FIyMzd3jqJOA-vvdhvFrMvNL2bWhfnliFKQ"
            await fetch(url, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Bearer ${token}`
                },
                body: JSON.stringify(this.transaccionData)
            })
                .then(response => {
                    if (!response.ok) {
                        throw new Error('Error en la solicitud: ' + response.statusText);
                    }
                    return response.json();
                })
                .then(data => {
                    this.clearData()
                    this.updateTable()
                    console.log('Respuesta de la API:', data);
                })
                .catch(error => {
                    console.error('Error:', error);
                });
        },
        async updateTable() {
            const url = "http://127.0.0.1:8000/transacciones/"
            const token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJOb21icmVfVXN1YXJpbyI6IkFsZGFpciIsIkNvcnJlb19FbGVjdHJvbmljbyI6InN0cmluZyIsIkNvbnRyYXNlbmEiOiIxMjMiLCJOdW1lcm9fVGVsZWZvbmljb19Nb3ZpbCI6InN0cmluZyJ9.5EsBwNW9FIyMzd3jqJOA-vvdhvFrMvNL2bWhfnliFKQ"

            const response = await fetch(url, {
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Bearer ${token}`
                }
            });
            
            if (!response.ok) {
                throw new Error('Error en la solicitud: ' + response.statusText);
            }

            const data = await response.json();
            console.log('Respuesta de la API:', data);
            
            this.transaccionesTable = data.map(item => ({ ...item }));
            console.log('Table:', this.transaccionesTable);
        }
    },
    created() {
        this.updateTable()
    }
}
   
</script>
