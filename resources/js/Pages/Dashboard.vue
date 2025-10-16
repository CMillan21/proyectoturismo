<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';

// Simulación de datos para la tabla (eventualmente vendrán de Laravel)
const centrosTuristicos = [
    { id: 1, name: 'Tuxtepec', last_name: 'Rivera', country: 'México' },
    { id: 2, name: 'Soteapan', last_name: 'Montaña', country: 'México' },
    { id: 3, name: 'Catemaco', last_name: 'Laguna', country: 'México' },
];

// Funciones de ejemplo (solo imprimen en consola por ahora)
const editarCentro = (id) => {
    alert(`Modifique los datos que necesite: ${id}`);
    // Aquí iría la llamada a la API de Laravel: axios.get('/api/reportes/pdf/' + id)
};

// Funciones de ejemplo (solo imprimen en consola por ahora)
const generarPDF = (id) => {
    alert(`Generando reporte PDF para Centro ID: ${id}`);
    // Aquí iría la llamada a la API de Laravel: axios.get('/api/reportes/pdf/' + id)
};

const eliminarCentro = (id) => {
    if (confirm(`¿Estás seguro de ELIMINAR el Centro ID ${id}?`)) {
        alert(`Eliminando Centro ID: ${id}`);
        // Aquí iría la llamada a la API de Laravel: router.delete(route('centros.destroy', id))
    }
};
</script>

<template>
    <Head title="Panel" />

    <AuthenticatedLayout>
        <template #header>Panel de administración</template> 

        <div class="bg-white shadow overflow-hidden rounded-lg p-6">
            <h2 class="text-2xl font-bold text-gray-800 mb-4">
                Gestión de Centros Turísticos
            </h2>

            <div class="overflow-x-auto">
                <table class="min-w-full divide-y divide-gray-200">
                    <thead class="bg-gray-50">
                        <tr>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">#</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Nombre</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Propietario</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Última modificación</th>
                            <th class="px-6 py-3 text-center text-xs font-medium text-gray-500 uppercase tracking-wider">Acciones</th>
                        </tr>
                    </thead>
                    <tbody class="bg-white divide-y divide-gray-200">
                        <tr v-for="centro in centrosTuristicos" :key="centro.id">
                            <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">{{ centro.id }}</td>
                            <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{{ centro.name }}</td>
                            <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{{ centro.last_name }}</td>
                            <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{{ centro.country }}</td>
                            <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-center space-x-2">
                                
                                <button class="text-blue-600 hover:text-blue-900 bg-gray-100 p-2 rounded-full">
                                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path></svg>
                                </button>


                                <button @click="editarCentro(centro.id)" class="text-yellow-600 hover:text-yellow-900 bg-yellow-100 p-2 rounded-full">
                                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.284-8.284z"></path></svg>
                                </button>
                                
                                <button @click="generarPDF(centro.id)" class="text-red-600 hover:text-red-900 bg-red-100 p-2 rounded-full">
                                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 21h10a2 2 0 002-2V9.414a1 1 0 00-.293-.707l-5.414-5.414A1 1 0 0012.586 3H7a2 2 0 00-2 2v14a2 2 0 002 2z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 3v5a1 1 0 001 1h5"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 16h6M9 12h6M9 8h6"></path></svg>
                                </button>


                                <button @click="eliminarCentro(centro.id)" class="text-white hover:bg-red-700 bg-red-600 p-2 rounded-full shadow-md">
                                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg>
                                </button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </AuthenticatedLayout>
</template>