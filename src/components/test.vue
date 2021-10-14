<template>
  <div class="container m-auto text-center">
    <img class="w-25" alt="img_pokemon" src="./assets/logo2.png" />
    <h2>PokeGuía</h2>
    <form>
      <div class="mb-3">
        <label for="nombre" class="form-label">Nombre</label>
        <input
          type="text"
          class="form-control w-25 m-auto"
          id="nombre"
          v-model="nombrePokemon"
          placeholder=""
          @keyup.enter="buscaPokemon"     
        />
     </div>
      <button type="button" @click="buscaPokemon" class="btn btn-primary">Buscar</button>
    </form>
  </div>

  
  <div class="container text-center">
    

    <div class="d-flex my-5">
      <div class="w-50 mx-3">
        <h4>{{ nombre }}</h4>
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
      dataPokemon: {
        name: "",
        sprites: {
          back_default: "",
        },
      },
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
      this.nombrePokemon = ''  
      return this.dataPokemon;
    },
  },
  computed: {
    nombre() {
      return this.dataPokemon.name;
    },
    imagen() {
      return this.dataPokemon.sprites.back_default;
    },
  },
};
</script>



<style>
</style>