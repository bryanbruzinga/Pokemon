<template>
  <div class="container">
    <h1><img src='https://upload.wikimedia.org/wikipedia/commons/9/98/International_Pok%C3%A9mon_logo.svg' alt="Pokemon"></h1>
    <div class="busca">
      <button @click="buscarPokemon(pokemonBuscado)">🔍</button>
      <label for="busca"></label>
      <input type="text" name="busca" placeholder="Digite um Pokemon para buscar..." v-model.lazy="pokemonBuscado">      
    </div>
    <div v-if="pokemonEncontrado">
      {{pokemonEncontrado.name}}
      <img class="pokeImg" :src="'https://pokeres.bastionbot.org/images/pokemon/' + pokemonBuscado + '.png'" :alt="pokemonEncontrado.name">
    </div>
  </div>
</template>

<script>
export default {
  name: "PokemonBusca",
  data() {
    return {
      pokemonBuscado: "",
      pokemonEncontrado: null
    }    
  },
  methods: {
    buscarPokemon(pokemonBuscado) {
      fetch(`https://pokeapi.co/api/v2/pokemon/${pokemonBuscado}`)
      .then(r => r.json())
      .then(json => {
        this.pokemonEncontrado = json
      })
    }
  },
}
</script>

<style scoped>
p {
  color: white;
}

.container {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-around;
}

img {
  position: relative;
  display: block;
  height: 110px;
  width: 250px;
}

.busca {
  width: 500px;
  position: relative;
  transition: all .5s;
}

.busca button {
  position: absolute;
  right: 10px;
  height: 100%;
  border: none;
  border-radius: 10px;
  background: none;
  cursor: pointer;
}

.busca:hover {
  background: white;
  transform: scale(1.1);
}

input {
  display: block;
  height: 40px;
  border: none;
  background: rgba(255, 255, 255, .9);
  width: 100%;
  border-radius: 10px;
  padding: 10px;
  transition: all .2s;
}

@media (max-width: 535px) {
  .container {
    display: flex;
    flex-direction: column;
  }
  .busca {
    max-width: 350px;
  }
}

</style>