<script lang="ts" setup>
const props = defineProps<{
  buttonCopy: string;
  link: string;
}>();

console.log("\nMenu Button:");
console.log("buttonCopy: ", props.buttonCopy);
console.log("buttonCopy: ", props.link);
</script>

<template ButtonProps>
  <a :href="props.link" class="MainMenuButtonWrapper">
    <div class="MainMenuButton">
      <img class="PokeballImage" src="../../assets/Pokeball.jpg" />
      <h2 class="ButtonCopy">
        {{ buttonCopy }}
      </h2>
    </div>
  </a>
</template>

<style scoped>
.MainMenuButtonWrapper {
  border: 1px solid red;

  background-image: url('../../assets/');
  justify-content: flex-start;
  align-items: center;
  margin: 20px 0px;
  display: flex;
  height: 75px;
  width: 300px;

  .MainMenuButton {
    justify-content: flex-start;
    align-items: center;
    display: flex;

    .PokeballImage {
      height: 50px;
    }

    .ButtonCopy {
      margin-left: 10px;
    }
  }
}
</style>
