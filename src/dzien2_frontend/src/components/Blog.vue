<template>
    <div>
        <h2 class="text-blue-600">Wpisy na bloga</h2>
        <div class="w-100 flex flex-row-reverse">
            <button @click ="pobierzWpisy" class="float-right bg-blue-600 rounded text-white p-4">Refresh</button>
        </div>
        <div class="grid mx-6 gap-4 my-4">
            <div v-for="(wpis,index) in wpisy" class="drop-shadow-x1 bg-stone-300 p-4">
                <p>id: {{ index }}</p>
                <p>{{ wpis }}</p>
                <button @click="usun_wpis(index)">Usuń</button>
            </div>
        </div>
        <div class="flex justify-center flex-col">
            <input v-model="nowyBlog" type="text" class="border-2 border-blue-600 p-4">
            <button @click="dodajWpis" class=" bg-blue-600 rounded text-white p-4">Dodaj</button>
        </div>
    </div>
</template>
<script>
import { dzien2_backend } from 'declarations/dzien2_backend/index';

    export default {
        data(){
            return{
                wpisy:[],
                nowyBlog: ""
            }
        },
        methods: {
            async pobierzWpisy(){
                this.wpisy = await dzien2_backend.odczytaj_wpisy();
            },
            async dodajWpis(){
                await dzien2_backend.dodaj_wpis(this.nowyBlog);
            },
            async usun_wpis(index){
                await dzien2_backend.usun_wpis(index);
            }
        },
        async mounted(){
            this.pobierzWpisy()
        }
    }
</script>