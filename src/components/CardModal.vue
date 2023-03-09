<template>
  <div>
    <b-modal id="cardPokemon" :title="detallesPokemon.name">
      <img :src="detallesPokemon.sprites.front_default" :alt="detallesPokemon.name" />
    </b-modal>
  </div>
</template>

<script>
export default {
  name: "CardModal",
  props: {
    detallesPokemon: Array
  }
};
</script>

<style>
</style>