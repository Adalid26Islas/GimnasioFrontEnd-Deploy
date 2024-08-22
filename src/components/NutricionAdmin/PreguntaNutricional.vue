<template>
    <main class="w-full ml-2">
        <table class="w-full">
            <thead>
                <tr>
                    <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-l-md">Pregunta</th>
                    <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Fecha de creacion</th>
                    <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100">Fecha de Actualización</th>
                    <th scope="col" class="px-6 py-4 bg-gray-900 font-medium text-gray-100 rounded-r-md"></th>
                </tr>
            </thead>
            <tbody>
                <tr>
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
                        <button type="button" id="editar" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                            Editar
                        </button>
                    </th>
                    <th class="flex justify-center">
                        <button type="button" id="eliminar" class="px-4 mt-1 py-2 rounded-md bg-red-600 text-white hover:bg-gray-600">
                            Eliminar
                        </button>
                    </th>
                </tr>
            </tbody>
        </table>
    </main>
</template>
