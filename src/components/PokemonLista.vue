<template>
    <div class="container">
      <div class="listaPokemons">
        <section class="pokemon" v-for="(pokemon, index) in pokemons" :key="'poke' + index" @click="puxarPokemon(pokemon.url)">
          <img :src="imgUrl + pokemon.id + '.png'" :alt="pokemon.name">
          <span class="pokemonID"># {{pokemon.id}}</span>
          <h3>{{pokemon.name}}</h3>
        </section>
      </div>
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
      pokemonsInnerSkills: [],
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
  display: flex;
  align-items: center;
  justify-content: center;
}

.listaPokemons {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  justify-content: center;
}

.pokemon {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 1rem;
  cursor: pointer;
  box-shadow: 5px 5px 15px rgba(0,0,0, .5);
  padding: 1.5rem;
  background: rgba(255, 255, 255, .8);
  border-radius: 20px;
  transition: all .5s;
}

.pokemon h3 {
  font-size: 1.7rem;
}

.pokemonID {
  margin-top: 0.5rem;
  font-weight: bold;
  color: grey;
}

.pokemon img {
  height: 180px;
  width: 180px;  
  background: white;
  border-radius: 30px;
}

.pokemon:hover {
  transform: scale(1.1);  
}

@media (max-width: 1250px) {
  .listaPokemons {
    grid-template-columns: 1fr 1fr 1fr;
  }
}

@media (max-width: 960px) {
  .listaPokemons {
    grid-template-columns: 1fr 1fr;
  }
}

@media (max-width: 645px) {
  .pokemon img {
    height: 120px;
    width: 120px;
  }
  .pokemon h3 {
    font-size: 1rem;
  }
}

@media (max-width: 500px) {
  .pokemon {
    margin: 1rem 0.5rem;
  }
  .listaPokemons {
    grid-template-columns: 1fr 1fr;
  }
  .pokemon img {
    height: 80px;
    width: 80px;
  }
}

</style>