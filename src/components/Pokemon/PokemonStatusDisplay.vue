<script lang="ts" setup>
const props = defineProps<{
  pokemonData: {};
}>();
</script>

<template>
  <div class="StatusDisplayContainer">
    {{ props.pokemonData }}
  </div>
</template>

<style>
.StatusDisplayContainer {
  border: 1px solid red;
  padding: 5px;
  height: 100%;
}
</style>
