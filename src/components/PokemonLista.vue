<template>
    <div class="container">
      <section class="pokemon" v-for="(pokemon, index) in pokemons" :key="'poke' + index" @click="puxarPokemon(pokemon.url)">
          <img class="pokeImg" :src="imgUrl + pokemon.id + '.png'" :alt="pokemon.name">
          <h3>{{pokemon.name}}</h3>
          {{console.log(pokemon.url)}}
      </section>
      <div id="scrollAtivar" ref="infinitescrolltrigger"></div>
    </div>
</template>

<script>
export default {
  props: [
    'imgUrl',
    'apiUrl',
    'loading',
    'pokemonUrl'
  ],
  data() {
    return {
      pokemons: [],
      puxarMaisPokemons: '',
      urlAtual: ''
    }
  },
  methods: {
    puxarDados() {
      this.loading = true;
      fetch(this.urlAtual)
      .then(r => {
        if(r.status === 200)
        return r.json();
      })
      .then(data => {
        this.puxarMaisPokemons = data.next
        data.results.forEach(pokemon => {
          pokemon.id = pokemon.url.split('/')
          .filter(part => {
            return !!part
          }).pop();
          this.pokemons.push(pokemon);
          this.loading = false;
        })
      })
      .catch((error) => {
        console.error(error)
      })
    },
    scrollAtivar() {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if(entry.intersectionRatio > 0 && this.puxarMaisPokemons) {
            this.next()
          }
        });
      });
      observer.observe(this.$refs.infinitescrolltrigger);
    },
    next() {
      this.urlAtual = this.puxarMaisPokemons;
      this.puxarDados();
    },
    puxarPokemon(url) {
      this.$emit('puxarPokemon', url);
    }
  },
  computed: {
    console: () => console
  },
  created() {
    this.urlAtual = this.apiUrl;
    this.puxarDados();    
  },
  mounted() {
    this.scrollAtivar();
  }
}
</script>

<style scoped>

.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  align-items: center;
  justify-content: center;
}

.pokemon {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 2rem;
  cursor: pointer;
  box-shadow: 5px 5px 15px rgba(0,0,0, .5);
  padding: 2rem;
  background: rgba(255, 255, 255, .8);
  border-radius: 20px;
  max-width: 250px;
  transition: all .5s;
}

.pokemon h3 {
  font-size: 1.7rem;
}

.pokemon img {
  height: 180px;
  width: 180px;  
  background: white;
  border-radius: 30px;
}

.pokemon:hover {
  transform: scale(1.2);  
}

@media (max-width: 1250px) {
  .container {
    grid-template-columns: 1fr 1fr 1fr;
  }
}

@media (max-width: 960px) {
  .container {
    grid-template-columns: 1fr 1fr;
  }
}

@media (max-width: 645px) {
  .container {
    display: flex;
    flex-direction: column;
    width: 100%;
  }
  .pokemon {
    width: 100%;
  }
  .pokemon img {
    height: 140px;
    width: 140px;
  }
}

</style>