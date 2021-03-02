<template>
  <div>
    <PokemonBusca/>
    <Loading v-if="loading"/>
    <PokemonLista :pokemonUrl="pokemonUrl" :loading="loading" :imgUrl="imgUrl" :apiUrl="apiUrl" @puxarPokemon="puxarPokemon"/>
    <PokemonDetalhes v-if="mostrarDetalhes" :pokemonUrl="pokemonUrl" :imgUrl="imgUrl" @fecharDetalhes="fecharDetalhes"/>
  </div>
</template>

<script>

import PokemonBusca from '@/components/PokemonBusca.vue';
import PokemonLista from '@/components/PokemonLista.vue';
import PokemonDetalhes from '@/components/PokemonDetalhes.vue';
import Loading from '@/components/Loading.vue';

export default {
  name: 'Pokemon',
  data() {
    return {
      imgUrl: 'https://pokeres.bastionbot.org/images/pokemon/',
      apiUrl: 'https://pokeapi.co/api/v2/pokemon/',
      pokemonUrl: '',
      mostrarDetalhes: false,
      loading: false
    }
  },
  components: {
    PokemonBusca,
    PokemonLista,
    PokemonDetalhes,
    Loading
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
