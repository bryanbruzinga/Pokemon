<template>
  <div class="container">
    <h1><img src='https://upload.wikimedia.org/wikipedia/commons/9/98/International_Pok%C3%A9mon_logo.svg' alt="Pokemon"></h1>
    <form @submit.prevent="puxarPokemon" class="busca">      
      <label for="busca">
        <button type="submit" @click="puxarPokemon">🔍</button>
      </label>
      <input type="text" name="busca" placeholder="Busque um pokemon" v-model="pokemonBuscado">      
    </form>

  </div>
</template>

<script>
export default {
  name: "PokemonBusca",
  props: [ 'apiUrl'],
  data() {
    return {
      pokemonBuscado: '',
    }    
  },
  methods: {
    puxarPokemon() {
      if (this.pokemonBuscado !== '') {
        this.$emit('puxarPokemon', this.apiUrl + this.pokemonBuscado);
      }
    }
  }
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

@media (max-width: 805px) {
  .container {
    display: flex;
    flex-direction: column;
  }
  .busca {
    max-width: 350px;
  }
}

</style>