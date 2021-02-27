<template>
    <div class="container">
      <section class="pokemon" v-for="(pokemon, index) in pokemons" :key="'poke' + index" @click="puxarPokemon(pokemon.url)">
          <h3>{{pokemon.name}}</h3>
          <img class="pokeImg" :src="imgUrl + pokemon.id + '.png'" :alt="pokemon.name">
      </section>
      <div id="scrollAtivar" ref="infinitescrolltrigger"></div>
    </div>
</template>

<script>
export default {
  props: [
    'imgUrl',
    'apiUrl'
  ],
  data() {
    return {
      pokemons: [],
      nextUrl: '',
      currentUrl: ''
    }
  },
  methods: {
    puxarDados() {
      fetch(this.currentUrl)
      .then(r => {
        if(r.status === 200)
        return r.json();
      })
      .then(data => {
        this.nextUrl = data.next
        data.results.forEach(pokemon => {
          pokemon.id = pokemon.url.split('/')
          .filter(part => {
            return !!part
          }).pop();
          this.pokemons.push(pokemon);
        })
      })
      .catch((error) => {
        console.error(error)
      })
    },
    scrollAtivar() {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if(entry.intersectionRatio > 0 && this.nextUrl) {
            this.next()
          }
        });
      });
      observer.observe(this.$refs.infinitescrolltrigger);
    },
    next() {
      this.currentUrl = this.nextUrl;
      this.puxarDados();
    },
    puxarPokemon(url) {
      this.$emit('puxarPokemon', url);
    }
  },
  created() {
    this.currentUrl = this.apiUrl;
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
  grid-template-columns: 1fr 1fr 1fr;
  align-items: center;
  justify-content: center;
  padding-top: 5rem;
}

.pokemon {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 2.5rem;
  cursor: pointer;
  box-shadow: 5px 5px 15px rgba(0,0,0, .5);
  padding: 2rem;
  background: rgba(255, 255, 255, .8);
  border-radius: 20px;
}

.pokemon h3 {
  font-size: 2rem;
}

.pokemon img {
  height: 180px;
  width: 180px;
  transition: all .5s;
}

.pokemon img:hover {
  transform: scale(1.4);  
}

@media (max-width: 960px) {
  .container {
    grid-template-columns: 1fr 1fr;
  }
}

@media (max-width: 645px) {
  .container {
    grid-template-columns: 1fr;
  }
  .pokemon img {
    height: 140px;
    width: 140px;
  }
}

</style>