<template>
    <div>
        <h2 class="text-blue-600">Wpisy na bloga:</h2>
        <div class="w-100 flex flex-row-reverse">
            <button @click="pobierzWpisy" class="bg-blue-600 rounded text-white p-4">refresh</button>
        </div>
        <div class="grid mx-6 gap-4 my-4">
            <div v-for="(wpis, index) in wpisy" class="drop-shadow-xl bg-stone-300 p-4">
                <p>id: {{ index }}</p>
                <p>{{ wpis }}</p>
                <br />
                <button  class="bg-blue-600 rounded text-white p-4" @click="deleteWpis(index)">usun</button>
                <br /><br />
                <label for="name">Nowy wpis:</label>
                <input type="text" id="name" v-model="nowywpis">
                <button  class="bg-blue-600 rounded text-white p-4 my-10" @click="aktualizuj(index)">aktualizuj</button>
                
            </div>
        </div>
        <div class="flex justify-center flex-col">
            <input v-model="nowyBlog" class="border-2 border-blue-600 p-4" type="text">
            <button  class="bg-blue-600 rounded text-white p-4" @click="dodajWpisy">dodaj</button>
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
            await this.pobierzWpisy();
        },
        async deleteWpis(index) {
            await dzien2_backend.usun_wpis(index);
            await this.pobierzWpisy();
        },
        async pobierzWpisy() {
            this.wpisy = await dzien2_backend.odczytaj_wpisy();
        },
        async aktualizujWpis(index, nowywpis) {
            
            
            await dzien2_backend.edytuj_wpis(index, nowywpis);
            await this.pobierzWpisy();
        },
        async aktualizuj(index)
        {
            
            await dzien2_backend.edytuj_wpis(index, this.nowywpis);
            await this.pobierzWpisy();
            
        }
    },
    async mounted(){
        this.pobierzWpisy()
    }
}
</script>