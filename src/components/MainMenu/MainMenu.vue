<script setup>
import CyberButton from "../Components/CyberButton.vue";
// import MenuButton from "./MenuButton.vue";
</script>

<template>
  <div class="MainMenuContainer">
    <div class="PokemonLogoContainer">
      <img src="./assets/Pokemon_Logo.png" />
      <div class="PokemonSubHeader">Gotta Catch 'em all</div>
    </div>

    <CyberButton buttonCopy="Pokemon" link="#/pokemon" glitchType />
    <CyberButton buttonCopy="Items" link="#/items" />
    <CyberButton buttonCopy="Berries" link="#/berries" glitchType />
  </div>
  <!-- <MenuButton buttonCopy="Pokemon" link="/pokemon" glitchType  />
  <MenuButton buttonCopy="Items" link="/items" />
  <MenuButton buttonCopy="Berries" link="/berries" glitchType /> -->
</template>

<style>
.MainMenuContainer {
  justify-content: center;
  flex-direction: row;
  align-items: center;
  display: flex;
  height: 100%:
  width: 100%:

  .PokemonLogoContainer {
    flex-direction: column;
    align-items: center;
    display: flex;

    img {
      height: 100px;
    }
  }
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
