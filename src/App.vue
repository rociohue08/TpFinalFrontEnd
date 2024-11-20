<script setup lang="ts">
import { reactive, ref } from 'vue'
import { useRoute } from 'vue-router'
import { MoonIcon, SunIcon, LinkIcon } from '@heroicons/vue/24/solid'
import { useThemeStore } from '@/stores/ThemeStore'
import { useSesionStore } from '@/stores/AuthSesionStore'

const useStore = useThemeStore() 
const theme =  reactive(useStore)

const sesionStore = useSesionStore()
const sesion = reactive(sesionStore)




</script>

<template>
  <div v-bind:class="theme.isDark ? 'dark' : ''" class="wrapper transition ease-linear">
    <div class="btn-wrapper z-10">
      <div class="toggle-btn flex items-center justify-center w-full my-4">
        <label for="toggle" class="flex items-center justify-center cursor-pointer">
          <div class="relative">
            <input type="checkbox" id="toggle" class="sr-only" @click="theme.toggleTheme"/>
            <div class="block bg-gray-600 w-14 h-8 rounded-full"></div>
            <div class="dot absolute left-1 top-1 bg-black w-6 h-6 flex items-center justify-center rounded-full transition">
              <!-- usar directiva v-if para mostrar el icono de luna o sol -->
              <MoonIcon v-if="!theme.isDark" class="w-4 h-4 text-white" />
              <SunIcon v-if="theme.isDark" class="w-full h-full text-yellow-500 p-1" />
            </div>
          </div>

          <!-- cambiar el texto segun sea Light o Dark mode -->
          <div v-bind:class="theme.isDark ? 'dark' : ''" class="label-text ml-2 font-medium">
            {{ theme.mode }}
          </div>
        </label>
      </div>
    </div>
    <div v-show="sesion.data?.user?.email===undefined? false : true" class="btn-wrapper-left z-10">
      <div class="toggle-btn flex items-center justify-center w-full my-4">
        <button @click="sesion.logout" :class="theme.isDark ? 'hover:bg-blue-100 focus:ring-blue-200 bg-blue-50' : 'hover:bg-blue-100'" class="w-full text-dark bg-blue-50 focus:ring-4 focus:outline-none focus:ring-primary-300 font-medium rounded text-sm px-5 py-3 text-center min-h-[32px]">
          Cerrar Sesion
        </button>
      </div>
    </div>
    <div v-bind:class="theme.isDark ? 'dark' : ''" class="img min-h-screen flex flex-col items-center transition"></div>
      <div class="todo lg:w-2/3 xl:w-2/5 w-full px-7">
        <RouterView />
      </div>
  </div>
  
  <!-- Footer -->
  <footer class="bg-gray-800 text-white py-3 mt-auto">
    <div class="container mx-auto text-center px-4">
      <p class="text-sm">Grupo: Rocío Hueñir y Mariano Leglise.</p>
      <div class="mt-4"></div>
    </div>
  </footer>

</template>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  height: 90vh; /* Asegura que el contenedor ocupe toda la altura de la pantalla */
  background: #fff;
}

.wrapper.dark {
  background: #434343;
}

.img {
  background-image: url('../src/assets/sol.jpg');
  background-position: top;
  background-repeat: no-repeat;
  background-size: contain;
}

.img.dark {
  background: url('../src/assets/noche2.jpg');
  background-position: top;
  background-repeat: no-repeat;
  background-size: contain;
}

.btn-wrapper {
  position: absolute;
  right: 16px;
}

.btn-wrapper-left {
  position: absolute;
  left: 16px;
}

input:checked~.dot {
  transform: translateX(100%);
  background-color: rgb(77, 148, 255);
}

.label-text {
  color: white;
}

.label-text.dark {
  color: black;
}

.todo {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translateX(-50%) translateY(-50%);
  z-index: 1000;
}

/* Estilos para el footer */
footer {
  position: relative;
  bottom: 0;
  width: 100%;
  background-color: #1f2937; /* Ajustar color de fondo si es necesario */
  text-align: center;
}

footer .container {
  max-width: 1200px;
  margin: 0 auto;
}
</style>
