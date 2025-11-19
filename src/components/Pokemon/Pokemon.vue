<script setup>
import GhostFunctionButton from "../Components/GhostFunctionButton.vue";
import PokemonStatusDisplay from "./PokemonStatusDisplay.vue";
import FunctionButton from "../Components/FunctionButton.vue";
import { onMounted, ref } from "vue";
import axios from "axios";

// Data
let displayPokemon = ref({});
let pokemonCount = ref(0);
let pokemonData = ref([]);

// Loading States
let loadingStatus = ref(true);
let loadingList = ref(true);

const changeHighlightedPokemon = async pokemonUrl => {
  console.log("clicked highlight Pokemon Fn Button with: ", pokemonUrl);
  await axios.get(pokemonUrl).then(res => {
    displayPokemon.value = res.data;
  });

  loadingStatus.value = false;
};

onMounted(async () => {
  console.log(`The component is now mounted.`);

  await axios
    .get("https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0")
    .then(res => {
      pokemonCount.value = res.data.count;
      pokemonData.value = res.data.results;

      // To take out - just for testing ghost state
      setTimeout(() => {
        loadingList.value = false;
      }, 3000);

      changeHighlightedPokemon(pokemonData.value[0].url);
    });
});
</script>

<template>
  <div class="PokemonPokedexContainer">
    <div class="PokemonInfoDisplayContainer">
      <PokemonStatusDisplay :pokemonData="displayPokemon" />
    </div>

    <div class="PokemonNameList">
      <ul>
        <template v-if="!loadingList && pokemonData.length">
          <li v-for="pokemon in pokemonData.slice(0, 10)" :key="pokemon.id">
            <FunctionButton
              :button-copy="pokemon.name"
              :pokemon-url="pokemon.url"
              emit-fn-name="changeHighlightedPokemon"
              @change-highlighted-pokemon="changeHighlightedPokemon" />
          </li>
        </template>

        <template v-else>
          <li v-for="_ in 20">
            <GhostFunctionButton />
          </li>
        </template>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.PokemonPokedexContainer {
  border: 2px solid blue;
  align-items: center;
  display: flex;
  height: 70vh;
  width: 100%;

  overflow: hidden;

  .PokemonInfoDisplayContainer {
    margin-right: 10px;
    width: 60%;
  }

  .PokemonNameList {
    justify-content: flex-start;
    flex-direction: column;
    align-items: flex-start;
    display: flex;
    height: 100%;

    ul {
      align-items: flex-start;
      flex-direction: column;
      overflow-y: scroll;
      display: flex;
      height: 100%;

      li {
        list-style: none;

        &:first-of-type .FunctionButtonWrapper,
        &:first-of-type .GhostFunctionButtonWrapper {
          margin-top: 10px;
        }
      }
    }
  }
}
</style>
