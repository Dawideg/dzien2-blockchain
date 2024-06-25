<template>
    <div>
        Siema
        <button @click="pobierzWpisy">Pobierz</button>
        {{wpisy}}
        <input v-model="nowyBlog" type="text">
        <button @click="dodajWpis">Dodaj</button>
    </div>
</template>
<script>
import { ref } from 'vue';
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
            }
        },
    }
</script>