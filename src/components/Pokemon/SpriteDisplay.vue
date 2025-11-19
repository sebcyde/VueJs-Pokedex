<script lang="ts" setup>
import { ref } from "vue";

const props = defineProps<{
  pokemonSpriteData: {
    front_default?: string;
    back_default?: string;
    front_female?: string;
    back_female?: string;
    front_shiny?: string;
    back_shiny?: string;
    front_shiny_female?: string;
    back_shiny_female?: string;
  };
}>();

let currentSprite = ref({});
</script>

<template>
  <div class="StatusDisplayContainer">
    <!-- <select @change="(event) => { console.log("Event: ", e) }"> -->

    <select>
      <option v-for="(url, spriteName) in pokemonSpriteData" :key="url">
        {{ spriteName }}
      </option>
    </select>

    <select v-model="selected" multiple>

      <!-- default -->
      <option
        selected
        v-if="pokemonSpriteData.front_default"
        value="front_default">
        Front
      </option>
      <option v-if="pokemonSpriteData.back_default" value="back_default">
        Back
      </option>

      <!-- female -->
      <option v-if="pokemonSpriteData.front_female" value="front_female">
        Female (Front)
      </option>
      <option v-if="pokemonSpriteData.back_female" value="back_female">
        Female (Back)
      </option>

      <!-- shiny -->
      <option v-if="pokemonSpriteData.front_shiny" value="front_shiny">
        Front (Shiny)
      </option>
      <option v-if="pokemonSpriteData.back_shiny" value="back_shiny">
        B (Shiny)
      </option>

      <!-- shiny female -->
      <option
        v-if="pokemonSpriteData.front_shiny_female"
        value="front_shiny_female">
        Front (Shiny Female)
      </option>
      <option
        v-if="pokemonSpriteData.back_shiny_female"
        value="back_shiny_female">
        Back (Shiny Female)
      </option>
    </select>
  </div>
</template>

<style>
.StatusDisplayContainer {
  border: 1px solid red;
  padding: 5px;
  height: 100%;
}
</style>
