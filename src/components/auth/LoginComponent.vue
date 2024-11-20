<script setup lang="ts">
import { reactive } from 'vue'
import { useThemeStore } from '@/stores/ThemeStore'
import { useSesionStore } from '@/stores/AuthSesionStore'

import type { CredentialsModel } from '@/models/CredentialsModel.ts'

import SpinnerComponent  from '@/components/SpinnerComponent.vue'

const useTheme = useThemeStore() 
const theme = reactive(useTheme)

const useSesion = useSesionStore()
const sesion = reactive(useSesion)

const credentials: CredentialsModel = {
    email: '',
    password: ''
}

const reactiveCredentials = reactive(credentials)

sesion.changeCrsfToken()
async function loginWithCredentials() {
    const response = await sesion.login(credentials)
}

</script>

<template>
    <div class="flex justify-center items-center min-h-[130px]">
        <div class="p-4 space-y-3 md:space-y-4 sm:p-6 max-w-[130px]">
            <h1 
                :class="theme.isDark ? 'text-blue-100' : 'text-gray-900'" 
                class="text-lg font-semibold leading-tight tracking-tight md:text-xl text-center"
            >
                Ingresa Con Tu Cuenta
            </h1>
        </div>
        <form 
            @submit.prevent="loginWithCredentials()" 
            class="p-4 space-y-3 md:space-y-4 sm:p-6 max-w-[400px]" 
            action="#"
        >
            <!-- Campo Email -->
            <div>
                <label 
                    :class="theme.isDark ? 'text-blue-100' : 'text-gray-900'" 
                    for="email" 
                    class="block mb-2 text-sm font-medium"
                >
                    Tu Email
                </label>
                <input 
                    v-model="reactiveCredentials.email" 
                    :class="theme.isDark ? 'bg-gray-700 border-gray-600 placeholder-gray-400 text-white focus:ring-blue-500 focus:border-blue-500' : 'bg-gray-50 border-gray-300 text-gray-900'" 
                    type="email" 
                    name="email" 
                    id="email" 
                    class="border text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2" 
                    placeholder="ejemplo@hotmail.com" 
                    required
                >
            </div>
            
            <!-- Campo Password -->
            <div>
                <label 
                    :class="theme.isDark ? 'text-blue-100' : 'text-gray-900'" 
                    for="password" 
                    class="block mb-2 text-sm font-medium"
                >
                    Password
                </label>
                <input 
                    v-model="reactiveCredentials.password" 
                    :class="theme.isDark ? 'bg-gray-700 border-gray-600 placeholder-gray-400 text-white focus:ring-blue-500 focus:border-blue-500' : 'bg-gray-50 border-gray-300 text-gray-900'" 
                    type="password" 
                    name="password" 
                    id="password" 
                    class="border text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2" 
                    placeholder="••••••••" 
                    required
                >
            </div>
            
            <!-- Botón de Enviar -->
            <button 
                type="submit" 
                :class="theme.isDark ? 'hover:bg-violet-700 focus:ring-violet-800 bg-violet-600' : 'hover:bg-violet-700'" 
                class="flex flex-row justify-center w-full text-white bg-violet-600 focus:ring-4 focus:outline-none focus:ring-primary-300 font-medium rounded text-sm px-4 py-2 text-center"
            >
                <p v-show="!sesion.loading" class="my-auto p-0 text-center">Ingresar</p>
                <SpinnerComponent v-show="sesion.loading" class="my-auto"/>
            </button>
            
            <!-- Mensaje de Error -->
            <small 
                v-if="sesion.error === '' ? false : true" 
                class="text-center text-red-500 text-sm"
            >
                {{ sesion.error }}
            </small>
        </form>
    </div>
</template>


<style scoped>

</style>