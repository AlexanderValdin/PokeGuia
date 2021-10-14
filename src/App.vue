<template>
  <div class="container m-auto text-center">
    <h1 class="">PokeGuía</h1>
    <label for="nombre">Nombre </label>
    <input
      type="text"
      v-model="nombrePokemon"
      :placeholder="dataPokemon.name"
    />
    <button type="button" @click="buscaPokemon">Buscar</button>
  </div>
  <div class="container text-center">
    <h3>{{ dataPokemon.name }}</h3>

    <div class="d-flex my-5">
      <div class="w-50 mx-3">
        <h4>Imagen</h4>
        <img
          class="border"
          alt="pokemon"
          :src="dataPokemon.sprites.back_default"
        />
      </div>

      <ul class="list-group w-50 mx-3">
        <h4>Habilidades</h4>
        <li
          class="list-group-item"
          v-for="(item, index) of dataPokemon.abilities"
          :key="index"
        >
          {{ item.ability.name }}
        </li>
      </ul>

      <ul class="list-group w-50 mx-3">
        <h4>Movimientos</h4>
        <li
          class="list-group-item"
          v-for="(item, index) of dataPokemon.moves"
          :key="index"
        >
          {{ item.move.name }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      nombrePokemon: "",
      defaultPokemon: "pikachu",
      dataPokemon: "",
    };
  },
  created() {
    console.log("carga Created");
    fetch("https://pokeapi.co/api/v2/pokemon/" + this.defaultPokemon)
      .then((response) => response.json())
      .then((response) => (this.dataPokemon = response));
  },
  methods: {
    buscaPokemon() {
      fetch("https://pokeapi.co/api/v2/pokemon/" + this.nombrePokemon)
        .then((response) => response.json())
        .then((response) => (this.dataPokemon = response));
      return this.dataPokemon;
    },
  },
};
</script>



<style>
</style>