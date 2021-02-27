<template>
  <div>
    <PokemonBusca />
    <PokemonLista :imgUrl="imgUrl" :apiUrl="apiUrl" @puxarPokemon="puxarPokemon"/>
    <PokemonDetalhes v-if="mostrarDetalhes" :pokemonUrl="pokemonUrl" :imgUrl="imgUrl" @fecharDetalhes="fecharDetalhes"/>
  </div>
</template>

<script>

import PokemonBusca from '@/components/PokemonBusca.vue';
import PokemonLista from '@/components/PokemonLista.vue';
import PokemonDetalhes from '@/components/PokemonDetalhes.vue';

export default {
  name: 'Pokemon',
  data() {
    return {
      imgUrl: 'https://pokeres.bastionbot.org/images/pokemon/',
      apiUrl: 'https://pokeapi.co/api/v2/pokemon/',
      pokemonUrl: '',
      mostrarDetalhes: false
    }
  },
  components: {
    PokemonBusca,
    PokemonLista,
    PokemonDetalhes
  },
  methods: {
    puxarPokemon(url) {
      this.pokemonUrl = url;
      this.mostrarDetalhes = true;
    },
    fecharDetalhes() {
      this.pokemonUrl = '';
      this.mostrarDetalhes = false;
    }
  },
}

</script>

<style>

</style>
