<script setup>
import FunctionButton from "../Components/FunctionButton.vue";
import { onMounted, ref } from "vue";
import axios from "axios";

let displayPokemon = ref({});
let pokemonCount = ref(0);
let pokemonData = ref([]);

const changeHighlightedPokemon = async pokemonUrl => {
  console.log("clicked highlight Pokemon Fn Button with: ", pokemonUrl);
  await axios.get(pokemonUrl).then(res => {
    displayPokemon.value = res.data;
  });
};

onMounted(async () => {
  console.log(`the component is now mounted.`);

  await axios
    .get("https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0")
    .then(res => {
      pokemonCount.value = res.data.count;
      pokemonData.value = res.data.results;

      changeHighlightedPokemon(pokemonData.value[0].url);
    });
});
</script>

<template>
  <div class="PokemonPokedexContainer">
    Pokemon Template

    <div class="PokemonInfoDisplay">
      <!-- {{ pokemonData.value }} -->
    </div>

    <div class="PokemonNameList">
      <ul>
        <li v-for="pokemon in pokemonData.slice(0, 10)">
          <FunctionButton
            :button-copy="pokemon.name"
            :pokemon-url="pokemon.url"
            :emit-fn-name="'changeHighlightedPokemon'"
            @change-highlighted-pokemon="changeHighlightedPokemon" />
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
ul {
  li {
    list-style: none;
  }
}
</style>
