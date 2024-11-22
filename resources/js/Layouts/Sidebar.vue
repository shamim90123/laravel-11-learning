<template>
    <aside class="w-64 bg-white h-full shadow-lg border-r border-gray-200">
        <div class="flex flex-col h-full">
            <!-- Logo -->
            <div class="flex items-center justify-center h-16 border-b border-gray-200">
                <Link :href="route('dashboard')">
                    <img src="/logo.png" alt="Logo" class="h-10 w-auto">
                </Link>
            </div>

            <!-- Navigation Links -->
            <nav class="flex-1 px-4 py-4 space-y-2">
                <NavLink :href="route('dashboard')" :active="route().current('dashboard')">
                    Dashboard
                </NavLink>
                <NavLink :href="route('projects.index')" :active="route().current('projects.index')">
                    Projects
                </NavLink>
                <NavLink :href="route('settings')" :active="route().current('settings')">
                    Settings
                </NavLink>
            </nav>

            <!-- Logout -->
            <div class="p-4 border-t border-gray-200">
                <form @submit.prevent="$emit('logout')">
                    <button type="submit" class="block w-full px-4 py-2 text-left text-gray-700 hover:bg-gray-100 rounded-md">
                        Log Out
                    </button>
                </form>
            </div>
        </div>
    </aside>
</template>

<script setup>
import { Link, router } from '@inertiajs/vue3';
</script>
