<template>
  <div>
    <PokemonBusca :apiUrl="apiUrl" @puxarPokemon="puxarPokemon"/>
    <Loading />
    <PokemonLista :imgUrl="imgUrl" :apiUrl="apiUrl" @puxarPokemon="puxarPokemon"/>
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
:root {
  --normal: #B5B2AB;
  --bug: #B6C64C;
  --poison: #A5609A;
  --psychic: #E864A5;
  --grass: #84C964;
  --ground: #DABF6D;
  --ice: #8ADEFC;
  --fire: #ED514A;
  --rock: #C0B176;
  --dragon: #8877EA;
  --water: #4FA5FA;
  --dark: #896A57;
  --fighting: #B76055;
  --ghost: #7774C0;
  --steel: #B7B7C9;
  --flying: #709EF2;
  --electric: #F4D35C;
  --fairy: #E6A5E7;
}

</style>
