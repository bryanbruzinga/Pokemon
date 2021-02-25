<template>
  <div class="container">
    <section class="pokemon" v-for="(pokemon, index) in pokemons" :key="'poke' + index" @click="puxarPokemon(pokemon.url)">
        <h3>{{pokemon.name}}</h3>
        <img class="pokeImg" :src="imgUrl + pokemon.id + '.png'" :alt="pokemon.name">
    </section>
    <div id="scrollAtivar" ref="infinitescrolltrigger">

    </div>
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
  justify-content: center
}

.pokemon {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-width: 400px;
  margin-bottom: 40px;
  cursor: pointer;
}

</style>