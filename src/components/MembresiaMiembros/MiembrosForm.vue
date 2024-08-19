<template>
    <h1 class="title-gym">BULL'S GYM</h1>
    <main class="w-[100%] h-auto ml-2">
        <section>
            <div class="mx-auto p-4">
                <div class="bg-white-900 white:bg-white-700 shadow rounded-lg p-6">
                    <h1 class="text-xl font-semibold mb-4 text-dark-100 dark:text-dark-100">Crear nueva meimbro</h1>
                    <p class="text-dark-100 dark:text-dark-100 mb-6">Ingresa la información correspondiente para crear una nueva meimbro.</p>
                    <form>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            <input type="number" placeholder="Miembro ID" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                            <input type="number" placeholder="Usuario ID" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            <select class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                                <option value="">Tipo de miembro</option>
                                <option value="nuevo">Nuevo</option>
                                <option value="frecuente">Frecuente</option>
                                <option value="ocasional">Ocasional</option>
                                <option value="esporadico">Esporádico</option>
                                <option value="visita">Visita</option>
                            </select>
                            <select class="rounded-lg w-full font-medium bg-gray-100 border border-gray-200 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                                <option value="">Estatus</option>
                                <option value="activo">Activo</option>
                                <option value="inactivo">Inactivo</option>
                            </select>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            <input type="text" placeholder="Antigüedad" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                            <input type="date" placeholder="Fecha de Registro" class="p-2 rounded-lg w-full font-medium bg-gray-100 border border-gray-200 placeholder-gray-500 text-sm focus:outline-none focus:border-gray-400 focus:bg-white">
                        </div>
                        <button type="button" id="membresia" class="px-4 py-2 w-[20%] rounded bg-red-600 text-white hover:bg-gray-600 focus:outline-none transition-colors">
                            Crear meimbro
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
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-l-md">meimbro ID</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Usuario ID</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Tipo</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Estatus</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Antigüedad</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Fecha de Registro</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Fecha de Actualización</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-r-md"></th>
                    </tr>
                </thead>
                <tbody class="bg-gray-200">
                    <!-- Fila 1 -->
                    <tr class="hover:bg-gray-500">
                        <td class="h-[50px] text-center">
                            <span>001</span>
                        </td>
                        <td class="text-center">
                            <span>1001</span>
                        </td>
                        <td class="text-center">
                            <span>Nuevo</span>
                        </td>
                        <td class="text-center">
                            <span>Activo</span>
                        </td>
                        <td class="text-center">
                            <span>6 meses</span>
                        </td>
                        <td class="text-center">
                            <span>2024-08-15</span>
                        </td>
                        <td class="text-center">
                            <span>2024-08-15</span>
                        </td>
                        <td class="flex justify-center">
                            <button type="button" id="membresia" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar
                            </button>
                        </td>
                    </tr>
                    <!-- Fila 2 -->
                    <tr class="hover:bg-gray-500">
                        <td class="h-[50px] text-center">
                            <span>002</span>
                        </td>
                        <td class="text-center">
                            <span>1002</span>
                        </td>
                        <td class="text-center">
                            <span>Frecuente</span>
                        </td>
                        <td class="text-center">
                            <span>Inactivo</span>
                        </td>
                        <td class="text-center">
                            <span>12 meses</span>
                        </td>
                        <td class="text-center">
                            <span>2024-01-10</span>
                        </td>
                        <td class="text-center">
                            <span>2024-06-10</span>
                        </td>
                        <td class="flex justify-center">
                            <button type="button" id="membresia" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar
                            </button>
                        </td>
                    </tr>
                    <!-- Fila 3 -->
                    <tr class="hover:bg-gray-500">
                        <td class="h-[50px] text-center">
                            <span>003</span>
                        </td>
                        <td class="text-center">
                            <span>1003</span>
                        </td>
                        <td class="text-center">
                            <span>Ocasional</span>
                        </td>
                        <td class="text-center">
                            <span>Activo</span>
                        </td>
                        <td class="text-center">
                            <span>3 meses</span>
                        </td>
                        <td class="text-center">
                            <span>2024-05-01</span>
                        </td>
                        <td class="text-center">
                            <span>2024-08-01</span>
                        </td>
                        <td class="flex justify-center">
                            <button type="button" id="membresia" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar
                            </button>
                        </td>
                    </tr>
                    <!-- Fila 4 -->
                    <tr class="hover:bg-gray-500">
                        <td class="h-[50px] text-center">
                            <span>004</span>
                        </td>
                        <td class="text-center">
                            <span>1004</span>
                        </td>
                        <td class="text-center">
                            <span>Esporádico</span>
                        </td>
                        <td class="text-center">
                            <span>Activo</span>
                        </td>
                        <td class="text-center">
                            <span>1 año</span>
                        </td>
                        <td class="text-center">
                            <span>2023-08-15</span>
                        </td>
                        <td class="text-center">
                            <span>2024-08-15</span>
                        </td>
                        <td class="flex justify-center">
                            <button type="button" id="membresia" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar
                            </button>
                        </td>
                    </tr>
                    <!-- Fila 5 -->
                    <tr class="hover:bg-gray-500">
                        <td class="h-[50px] text-center">
                            <span>005</span>
                        </td>
                        <td class="text-center">
                            <span>1005</span>
                        </td>
                        <td class="text-center">
                            <span>Visita</span>
                        </td>
                        <td class="text-center">
                            <span>Inactivo</span>
                        </td>
                        <td class="text-center">
                            <span>6 meses</span>
                        </td>
                        <td class="text-center">
                            <span>2024-03-20</span>
                        </td>
                        <td class="text-center">
                            <span>2024-06-20</span>
                        </td>
                        <td class="flex justify-center">
                            <button type="button" id="membresia" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar
                            </button>
                        </td>
                    </tr>
                    <!-- Fila 6 -->
                    <tr class="hover:bg-gray-500">
                        <td class="h-[50px] text-center">
                            <span>006</span>
                        </td>
                        <td class="text-center">
                            <span>1006</span>
                        </td>
                        <td class="text-center">
                            <span>Nuevo</span>
                        </td>
                        <td class="text-center">
                            <span>Activo</span>
                        </td>
                        <td class="text-center">
                            <span>18 meses</span>
                        </td>
                        <td class="text-center">
                            <span>2023-12-01</span>
                        </td>
                        <td class="text-center">
                            <span>2024-06-01</span>
                        </td>
                        <td class="flex justify-center">
                            <button type="button" id="membresia" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar
                            </button>
                        </td>
                    </tr>
                </tbody>
            </table>
            <hr class="border-2 mt-4">
        </section>
    </main>
</template>
