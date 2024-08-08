<template>
    <main class="w-[100%] h-auto ml-2">
        <section>
            <div class="mx-auto p-4">
                <div class="bg-gray-200 dark:bg-gray-700 shadow rounded-lg p-6">
                    <h1 class="text-xl font-semibold mb-4 text-gray-900 dark:text-gray-100">Crear nueva dieta</h1>
                    <p class="text-gray-600 dark:text-gray-300 mb-6">Ingresa la información Correspondiente para crear una nueva dieta.</p>
                    <form>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                            <input type="text" placeholder="Nombre de usuario" class="border p-2 rounded w-full">
                            <input type="text" placeholder="Correo electronico del usuario" class="border p-2 rounded w-full">
                            <select class="border  rounded w-full">
                                <option value="">Sexo</option>
                                <option value="masculino">Masculino</option>
                                <option value="femenino">Femenino</option>
                            </select>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                            <input type="number" placeholder="Altura en Centimetros" class="border p-2 rounded w-full">
                            <input type="number" placeholder="Peso actual en Kilogramos" class="border p-2 rounded w-full">
                            <select class="border  rounded w-full">
                                <option value="">Objetivo de la dieta</option>
                                <option value="perdida">Perdida de peso</option>
                                <option value="aumento">Aumento de masa muscular</option>
                                <option value="mantenimiento">Mantenimiento</option>
                            </select>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                            <select class="border  rounded w-full">
                                <option value="">Tipo de Ejercicios Recomendados</option>
                                <option value="cardio">Cardio</option>
                                <option value="pesas">Levantamiento de pesas</option>
                                <option value="tecnicos">Ejercicios tecnicos</option>
                            </select>
                            <select class="border  rounded w-full">
                                <option value="">Dias de Ejercicio</option>
                                <option value="cardio">1 dia a la semana</option>
                                <option value="cardio">2 dias a la semana</option>
                                <option value="cardio">3 dias a la semana</option>
                                <option value="cardio">4 dias a la semana</option>
                                <option value="cardio">5 dias a la semana</option>
                            </select>
                            <input type="number" placeholder="Calorias diarias" class="border p-2 rounded w-full">
                        </div>
                        <textarea name="" id="" cols="30" class="w-full mb-6 rounded-lg" placeholder="Alimentos recomendados, restricciones u observaciones"></textarea>
                        <button type="button" id="dieta" class="px-4 py-2 rounded bg-red-600 text-white hover:bg-gray-600 focus:outline-none transition-colors">
                            Crear dieta
                        </button>
                    </form>
                </div>
            </div>
        </section>
        <section class="bg-green-200">
            <div class="mx-auto">
                <h2>Seccion donde se mostrara la lista de dietas</h2>
            </div>
        </section>
    </main>
</template>