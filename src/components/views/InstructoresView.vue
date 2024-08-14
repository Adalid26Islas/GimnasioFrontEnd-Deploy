<template>
    <div class="grid sm:grid-cols-2 items-start gap-16 p-4 mx-auto max-w-4xl bg-white font-[sans-serif]">
        <!-- Sección de texto e imagen -->
        <div>
            <h1 class="text-gray-800 text-3xl font-extrabold">Registro de Instructores</h1>
            <p class="text-sm text-gray-500 mt-4">Complete el formulario para registrar un nuevo instructor en el sistema.</p>
            <!-- Imagen del instructor -->
            <div class="mt-8">
                <img src="https://c8.alamy.com/comp/DRRP55/young-fitness-instructor-gym-people-spinning-DRRP55.jpg" alt="Imagen del Instructor"
                    class="w-full h-auto rounded-lg shadow-md" />
            </div>
        </div>

        <!-- Formulario -->
        <form class="ml-auto space-y-4">
            <!-- Campo de carga de fotografía -->
            <div>
                <label for="fotografia" class="block text-gray-700 text-sm font-medium">Fotografía</label>
                <input type="file" id="fotografia" accept="image/*"
                    class="w-full rounded-md py-3 px-4 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            </div>
            <input type='text' placeholder='ID'
                class="w-full rounded-md py-3 px-4 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            <input type='number' placeholder='Total Años de Experiencia'
                class="w-full rounded-md py-3 px-4 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            <input type='text' placeholder='Especialidad'
                class="w-full rounded-md py-3 px-4 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            <input type='number' placeholder='Total Clientes Atendidos'
                class="w-full rounded-md py-3 px-4 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            <select placeholder='Estatus'
                class="w-full rounded-md py-3 px-4 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent">
                <option value="">Selecciona Estatus</option>
                <option value="Activo">Activo</option>
                <option value="Inactivo">Inactivo</option>
            </select>
            <input type='number' placeholder='Calificación' max="5" min="0" step="0.1"
                class="w-full rounded-md py-3 px-4 bg-gray-100 text-gray-800 text-sm outline-blue-500 focus:bg-transparent" />
            <button type='button'
                class="text-white bg-red-500 hover:bg-blue-600 tracking-wide rounded-md text-sm px-4 py-3 w-full !mt-6">Registrar</button>
        </form>
    </div>

    <div class="mt-12 w-full">
        <TableInstructores></TableInstructores>
    </div>
</template>

<script>
    import Persona from '../../components/Persona.vue'
    import TableInstructores from '../../components/TableInstructores.vue';

    export default {
        components: {
            Persona,
            TableInstructores,
        }
    }
</script>
