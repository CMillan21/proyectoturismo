<script setup>
// Importa usePage de Inertia
import { ref, computed } from 'vue'; 
import { Link, usePage } from '@inertiajs/vue3'; // <-- IMPORTACIÓN CLAVE

import Dropdown from '@/Components/Dropdown.vue';
import DropdownLink from '@/Components/DropdownLink.vue';

const showingNavigationDropdown = ref(false);

// 1. Obtiene la referencia al objeto $page
const page = usePage(); 

// 2. Accede al usuario de forma segura usando 'page'
const user = computed(() => page.props.auth.user); 

// Si usaste esta línea en tu código original, elimínala o corrígela:
// const user = $page.props.auth.user; 

</script>

<template>
    <div class="flex h-screen bg-gray-50">
        <aside class="w-64 flex-shrink-0 bg-blue-900 text-white shadow-lg">
            <div class="py-4 text-center text-xl font-semibold border-b border-blue-700">
                Turismo comunitario
            </div>
            
            <nav class="mt-6">
                <Link
                    :href="route('dashboard')"
                    :class="{ 'bg-blue-900': route().current('dashboard') }"
                    class="flex items-center space-x-4 px-6 py-3 transition duration-150 ease-in-out hover:bg-blue-700"
                >
                
            <!--icono dashboard-->
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="m2.25 12 8.954-8.955c.44-.439 1.152-.439 1.591 0L21.75 12M4.5 9.75v10.125c0 .621.504 1.125 1.125 1.125H9.75v-4.875c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125V21h4.125c.621 0 1.125-.504 1.125-1.125V9.75M8.25 21h8.25" />
                </svg>
                    
                    <span>Dashboard</span>
                </Link>

                <!--
                <Link
                    :href="route('centros.index')"
                    :class="{ 'bg-purple-900': route().current('centros.index') }"
                    class="flex items-center space-x-4 px-6 py-3 transition duration-150 ease-in-out hover:bg-purple-700"
                >
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path></svg>
                    <span>Centros Turísticos</span>
                </Link>
                -->



                <!--
                <Link
                    :href="route('logout')"
                    method="post"
                    as="button"
                    class="flex items-center space-x-4 px-6 py-3 mt-4 w-full transition duration-150 ease-in-out hover:bg-purple-700"
                >
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"></path></svg>
                    <span>Cerrar Sesión</span>
                </Link>
                -->


            </nav>
        </aside>



        <div class="flex flex-col flex-1 overflow-y-auto">
            <header class="bg-white shadow-md flex justify-between items-center h-16 px-6">
                <div class="text-xl font-semibold text-gray-800">
                    <slot name="header" />
                </div>
                
                <Dropdown align="right" width="48">
                    <template #trigger>
                        <button type="button" class="text-sm font-medium text-gray-600 hover:text-gray-900 focus:outline-none flex items-center">
                            {{ user.name }}
                            <svg class="ms-2 h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd"/></svg>
                        </button>
                    </template>
                    <template #content>
                        <!--Inabilitamos el botón de edición de cuenta-->
                        <!--<DropdownLink :href="route('profile.edit')">Perfil</DropdownLink>-->
                        <DropdownLink :href="route('logout')" method="post" as="button">Cerrar sesión</DropdownLink>
                    </template>
                </Dropdown>
            </header>

            <main class="p-6">
                <slot/>
            </main>
        </div>
    </div>
</template>