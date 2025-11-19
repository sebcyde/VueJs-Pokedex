<script setup>
import { ref, computed } from "vue";

import NotFound from "./components/NotFound/NotFound.vue";
import MainMenu from "./components/MainMenu/MainMenu.vue";
import Pokemon from "./components/Pokemon/Pokemon.vue";
import Berries from "./components/Berries/Berries.vue";
import Items from "./components/Items/Items.vue";

const routes = {
  "/": MainMenu,
  "/pokemon": Pokemon,
  "/items": Items,
  "/berries": Berries,
};

const currentPath = ref(window.location.hash);

window.addEventListener("hashchange", () => {
  console.log("hashchange: ", window.location.hash);
  currentPath.value = window.location.hash;
});

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || "/"] || NotFound;
});
</script>

<template>
  <component :is="currentView" />
</template>

<style scoped>
.App {
  width: auto;
  height: auto;
  background-image: url("./assets/BG_1.jpg");
  background-color: blue;
}
</style>
