<template>
  <main class="min-h-[87vh] ml-2 w-full">
    

<!-- Modal toggle -->
<button data-modal-target="crud-modal" data-modal-toggle="crud-modal" class="px-4 mt-1 py-2 font-medium rounded-md bg-red-600 text-white hover:bg-gray-600 mb-4" type="button">
  Insertar nueva pregunta nutricional
</button>

<!-- Main modal -->
<div id="crud-modal" tabindex="-1" aria-hidden="true" class="hidden overflow-y-auto overflow-x-hidden fixed top-0 right-0 left-0 z-50 justify-center items-center w-full md:inset-0 h-[calc(100%-1rem)] max-h-full">
    <div class="relative p-4 w-full max-w-md max-h-full">
        <!-- Modal content -->
        <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
            <!-- Modal header -->
            <div class="flex items-center justify-between p-4 md:p-5 border-b rounded-t dark:border-gray-600">
                <h3 class="text-lg font-semibold text-gray-900 dark:text-white">
                    Agregar nueva pregunta nutricional
                </h3>
                <button type="button" class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 ms-auto inline-flex justify-center items-center dark:hover:bg-gray-600 dark:hover:text-white" data-modal-toggle="crud-modal">
                    <svg class="w-3 h-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 14">
                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6"/>
                    </svg>
                    <span class="sr-only">Close modal</span>
                </button>
            </div>
            <!-- Modal body -->
            <form class="p-4 md:p-5">
                <div class="grid gap-4 mb-4 grid-cols-2">
                    <div class="col-span-2">
                        <label for="name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Pregunta</label>
                        <input type="text" name="name" id="name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500" placeholder="¿?">
                    </div>
                </div>
                <button type="submit" class="text-white inline-flex items-center bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
                    <svg class="me-1 -ms-1 w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10 5a1 1 0 011 1v3h3a1 1 0 110 2h-3v3a1 1 0 11-2 0v-3H6a1 1 0 110-2h3V6a1 1 0 011-1z" clip-rule="evenodd"></path></svg>
                    Insertar pregunta
                </button>
            </form>
        </div>
    </div>
</div> 

    <table class="w-full bg-white text-left text-sm text-gray-900 rounded ">
                <thead class="bg-gray-50 text-center">
                    <tr>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-l-md">Pregunta</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Fecha de creacion</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Fecha de Actualización</th>
                        <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-r-md"></th>
                    </tr>
                </thead>
                <tbody class="bg-gray-200">
                    <tr class="hover:bg-gray-500 ">
                        <th class="h-[50px] text-center">
                            <span>¿Cuantos dias a la semana realizas ejercicios?</span>
                        </th>
                        <th class="text-center">
                            <span>03-Agosto-2024</span>
                        </th>
                        <th class="text-center">
                            <span>08-Agosto-2024</span>
                        </th>
                        <th class="flex justify-center">
                            <button type="button" id="dieta" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar pregunta
                            </button>
                        </th>
                    </tr>

                    <tr class="hover:bg-gray-500 ">
                        <th class="h-[50px] text-center">
                            <span>¿Cuantas comidas realizas al dia?</span>
                        </th>
                        <th class="text-center">
                            <span>03-Agosto-2024</span>
                        </th>
                        <th class="text-center">
                            <span>08-Agosto-2024</span>
                        </th>
                        <th class="flex justify-center">
                            <button type="button" id="dieta" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar pregunta
                            </button>
                        </th>
                    </tr>

                <!-- 

                    <tr class="hover:bg-gray-500">
                        <th class="h-[50px] text-center">
                            <span>aldair-NPM</span>
                        </th>
                        <th class="text-center">
                            <span>aldair_ai@gmail.com</span>
                        </th>
                        <th class="text-center">
                            <span>05-Agosto-2024</span>
                        </th>
                        <th class="text-center">
                            <span>08-Agosto-2024</span>
                        </th>
                        <th class="flex justify-center">
                            <button type="button" id="dieta" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar dieta
                            </button>
                        </th>
                    </tr>

                    <tr class="hover:bg-gray-500">
                        <th class="h-[50px] text-center">
                            <span>ameli_PG</span>
                        </th>
                        <th class="text-center">
                            <span>ameli_pg@gmail.com</span>
                        </th>
                        <th class="text-center">
                            <span>06-Agosto-2024</span>
                        </th>
                        <th class="text-center">
                            <span>08-Agosto-2024</span>
                        </th>
                        <th class="flex justify-center">
                            <button type="button" id="dieta" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar dieta
                            </button>
                        </th>
                    </tr>

                    <tr class="hover:bg-gray-500">
                        <th class="h-[50px] text-center">
                            <span>adalid_26</span>
                        </th>
                        <th class="text-center">
                            <span>adalid_iq@gmail.com</span>
                        </th>
                        <th class="text-center">
                            <span>03-Agosto-2024</span>
                        </th>
                        <th class="text-center">
                            <span>08-Agosto-2024</span>
                        </th>
                        <th class="flex justify-center">
                            <button type="button" id="dieta" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar dieta
                            </button>
                        </th>
                    </tr>

                    <tr class="hover:bg-gray-500">
                        <th class="h-[50px] text-center">
                            <span>emilio_MC</span>
                        </th>
                        <th class="text-center">
                            <span>emilio_mc@gmail.com</span>
                        </th>
                        <th class="text-center">
                            <span>04-Agosto-2024</span>
                        </th>
                        <th class="text-center">
                            <span>08-Agosto-2024</span>
                        </th>
                        <th class="flex justify-center">
                            <button type="button" id="dieta" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar dieta
                            </button>
                        </th>
                    </tr>

                    <tr class="hover:bg-gray-500">
                        <th class="h-[50px] text-center">
                            <span>aldair-NPM</span>
                        </th>
                        <th class="text-center">
                            <span>aldair_ai@gmail.com</span>
                        </th>
                        <th class="text-center">
                            <span>05-Agosto-2024</span>
                        </th>
                        <th class="text-center">
                            <span>08-Agosto-2024</span>
                        </th>
                        <th class="flex justify-center">
                            <button type="button" id="dieta" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar dieta
                            </button>
                        </th>
                    </tr>

                    <tr class="hover:bg-gray-500">
                        <th class="h-[50px] text-center">
                            <span>ameli_PG</span>
                        </th>
                        <th class="text-center">
                            <span>ameli_pg@gmail.com</span>
                        </th>
                        <th class="text-center">
                            <span>06-Agosto-2024</span>
                        </th>
                        <th class="text-center">
                            <span>08-Agosto-2024</span>
                        </th>
                        <th class="flex justify-center">
                            <button type="button" id="dieta" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                                Editar dieta
                            </button>
                        </th>
                    </tr> -->
                </tbody>
            </table>
            <hr class="border-2 mt-4">
  </main>
</template>