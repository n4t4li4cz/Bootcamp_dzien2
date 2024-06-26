<template>
    <div>
        <h2 class="text-color-600">Wpisy na bloga:</h2>
        <div class="w-100 flex flex-row-reverse">
            <button @click="pobierzWpisy" class="float-right bg-blue-600 rounded text-white p-4">refresh</button>
        </div>
        <div class="grid mx-6 gap-4 my-4 p-4">
        <div v-for="wpis in wpisy" class="drop-shadow-xl bg-stone-100">
            <p>{{wpis}}</p>
        </div>
        <div class="flex justifice-content flex-col">
            <input v-model="nowyBlog" type="text" class="borer-2 border-blue-600 p-4">
            <button @click="dodajWpisy" class="bg-blue-600 rounded text-white p-4">dodaj</button>

        </div>
        
    </div>
</div>
</template>

<script>
import { dzien2_backend } from 'declarations/dzien2_backend/index';

export default {
    data() {
        return {
            wpisy: [],
            nowyBlog: ""
        }
    },
    methods: {
        async dodajWpisy() {
            await dzien2_backend.dodaj_wpis(this.nowyBlog);
        },
        async pobierzWpisy() {
            this.wpisy = await dzien2_backend.odczytaj_wpisy();
        }
    },
    async mounted(){
        this.pobierzWpisy();
    }
}
</script>