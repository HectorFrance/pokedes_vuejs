<!-- SCRIPT -->
<script setup>
    import { onBeforeMount, onMounted, ref } from 'vue';

    let vetor = ref([]);

    let carregamento = ref(true)

    let filtro = ref('')

    onMounted(async () => {
        for (let i = 252; i <= 386; i++) {
            let requisicao = await fetch('https://pokeapi.co/api/v2/pokemon/' + i)
            let pokemon = await requisicao.json();
            vetor.value.push(pokemon);
        }

        carregamento.value = false;
    })

    function filtrar() {
        return vetor.value.filter(obj => obj.name.toLowerCase().includes(filtro.value.toLowerCase()));
    }
</script>

<!-- HTML -->
<template>

    <div class="carregamento" v-if="carregamento">
        <img src="../assets/loadpokegif.gif">
    </div>

    <main class="container" v-if="!carregamento">

        <!-- Filtragem -->
        <div class="row">
            <div class="col-12">
                <input type="text" placeholder="Qual pokemon esta procurando?" class="form-control pesquisa"
                    v-model="filtro">

                <p v-if="filtrar().length == 0">Não foi encontrado nenhum pokemon</p>
                <p v-else-if="filtrar().length == 1">Foi encontrado 1 pokemon</p>
                <p v-else> Foram encontrador {{ filtrar().length }} pokemons</p>
            </div>
        </div>

        <!-- Listagem -->
        <div class="row">
            <div class="col-12 col-sm-6 col-md-4 col-lg-3" v-for="v in filtrar()">
                <div class="card" :class="v.types[0].type.name">
                    <img :src="v.sprites.other.home.front_default">
                    <p>{{ v.name }}</p>
                </div>
            </div>
        </div>
    </main>
</template>