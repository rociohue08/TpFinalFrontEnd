<script setup lang="ts">
import {reactive} from 'vue'
import { TabGroup, TabList, Tab, TabPanels, TabPanel } from '@headlessui/vue'
import { useThemeStore } from '@/stores/ThemeStore';

import RegisterComponent  from '@/components/auth/RegisterComponent.vue'
import LoginComponent  from '@/components/auth/LoginComponent.vue'


const buttons = [
    {text: 'Ingreso', selected: true},
    {text: 'Registro', selected: false},
]

const btns = reactive(buttons)
const themeStore = useThemeStore()
const theme = reactive(themeStore)

function select() {
    if(btns[0].selected) {
        btns[0].selected = !btns[0].selected
    }
    else {
        btns[0].selected = !btns[0].selected
    }

    if(btns[1].selected) {
        btns[1].selected = !btns[1].selected
    }
    else {
        btns[1].selected = !btns[1].selected
    }
}

</script>


<template>
<div class="w-full px-2 py-2 sm:px-0">
    <TabGroup>
        <!-- Caja Principal -->
        <div 
    :class="theme.isDark ? 'bg-gray-700 text-violet-100' : 'bg-gray-200 text-violet-500'" 
    class="rounded shadow flex flex-col justify-between p-04" 
>
            <!-- Panels -->
            <TabPanels 
                :class="theme.isDark ? 'border-gray-700' : 'border-gray-200'" 
                class="flex-grow border p-4 rounded"
            >
                <TabPanel class="w-full">
                    <LoginComponent />
                </TabPanel>
                <TabPanel class="w-full">
                    <RegisterComponent />
                </TabPanel>
            </TabPanels>

            <!-- Tabs (Botones Abajo) -->
            <TabList
                :class="theme.isDark ? 'bg-violet/[0.12]' : 'bg-violet-900/20'" 
                class="flex justify-around py-1 mt-4 rounded"
            >
                <!-- Botones Iterables -->
                <Tab
                    @click="select()"
                    v-for="tab in buttons"
                    :key="tab.text"
                    :class="[tab.selected ? 'w-full bg-gray-300 rounded transition ease-linear' : 'rounded text-black-100 hover:bg-black/[0.12] hover:text-black', tab.selected&&theme.isDark ? 'bg-black-600 text-black-100' : 'text-black-500']" 
                    class="w-full focus:outline-none mx-1"
                >
                    <button class="px-10 py-3 mx-1 font-medium">{{ tab.text }}</button>
                </Tab>
            </TabList>
        </div>
    </TabGroup>
   </div>
</template>


<style scoped>

</style>
