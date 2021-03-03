<template>
  <div class="detalhes">
    <div class="verDetalhes" v-if="show">
      <div v-if="pokemon" class="imagem">
        <img :src="imgUrl + pokemon.id + '.png'" alt="pokemon.name" />
      </div>
      <div v-if="pokemon" class="data">
        <h2>{{ pokemon.name }}</h2>
        <div class="propriedades">
          <div class="left">Experiência Base</div>
          <div class="right">{{ pokemon.base_experience }} XP</div>
        </div>
        <div class="propriedades">
          <div class="left">Altura</div>
          <div class="right">{{ pokemon.height / 10 }} m</div>
        </div>
        <div class="propriedades">
          <div class="left">Peso</div>
          <div class="right">{{ pokemon.weight / 10 }} kg</div>
        </div>
        <h3>Tipo</h3>
        <div class="tipos">
          <div
            v-for="(tipo, index) in pokemon.types"
            :key="'tipo' + index"
            class=tipo
            :class=[tipo.type.name]
          >
            <p>{{ tipo.type.name }}</p>
          </div>
        </div>
        <h3>Habilidades</h3>
        <div class="habilidades">
          <div
            class="habilidade"
            v-for="(habilidade, index) in pokemon.abilities"
            :key="'habilidade' + index"
          >
            <p>{{ habilidade.ability.name }}</p>
          </div>
        </div>
      </div>
      <h2 v-else>O Pokemon não foi encontrado</h2>
      <button class="fechar" @click="fecharDetalhes">Fechar</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["pokemonUrl", "imgUrl"],
  data() {
    return {
      show: false,
      pokemon: {},
    };
  },
  methods: {
    puxarDados() {
      fetch(this.pokemonUrl)
        .then((r) => {
          if (r.status === 200) return r.json();
        })
        .then((data) => {
          this.pokemon = data;
          this.show = true;
        })
        .catch((error) => {
          console.error(error);
        });
    },
    fecharDetalhes() {
      this.$emit("fecharDetalhes");
    },
  },
  created() {
    this.puxarDados();
  },
};
</script>

<style scoped>
.detalhes {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, 0.7);
  animation: show-up .5s;
}
.verDetalhes {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  position: relative;
  width: 100%;
  max-width: 480px;
  padding: 3rem 0 0 0;
  background-color: #fafaf5;
}

.imagem {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: -80px;
  width: 150px;
  height: 150px;
  background: none;
  overflow: hidden;
}
.imagem img {
  width: 110px;
  height: 110px;
}

h2 {
  margin: 0.5rem 0;
}
.data {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  flex-direction: column;
  width: 100%;
  margin-bottom: 0.5rem;
}
.propriedades {
  width: 90%;
  max-width: 400px;
  border-bottom: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}
h3 {
  width: 100%;
  max-width: 400px;
  border-bottom: 1px solid #ccc;
}
.tipos,
.habilidades {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  width: 90%;
  max-width: 400px;
}
.habilidades {
  margin-bottom: 1rem;
}
.tipo,
.habilidade {
  padding: 0.2rem 1rem;
  border-radius: 10px;
  text-align: center;
  display: flex;
  align-items: center;
  color: #fff;
  font-size: 1.3rem;
}
.tipo {
  margin: 0 0.5rem;
}
.habilidade {
  margin: 0.5rem;
}
.bug {
  background-color: var(--bug);
}
.dark {
  background-color: var(--dark);
}
.dragon {
  background-color: var(--dragon);
}
.fire {
  background-color: var(--fire);
}
.flying {
  background-color: var(--flying);
}
.water {
  background-color: var(--water);
}
.grass {
  background-color: var(--grass);
}
.poison {
  background-color: var(--poison);
}
.normal {
  background-color: var(--normal);
}
.ghost {
  background-color: var(--ghost);
}
.psychic {
  background-color: var(--psychic);
}
.ice {
  background-color: var(--ice);
}
.fairy {
  background-color: var(--fairy);
}
.fighting {
  background-color: var(--fighting);
}
.ground {
  background-color: var(--ground);
}
.rock {
  background-color: var(--rock);
}
.electric {
  background-color: var(--electric);
}
.steel {
  background-color: var(--steel);
}
.habilidade {
  background-color: #c73015;
}
.fechar {
  border: 1px solid #3B5CA7;
  border-radius: 5px;
  background-color: #FFCB05;
  color: #3B5CA7;
  padding: 10px 20px;
  margin-bottom: 20px;
  font-size: 1.5rem;
  font-weight: bold;
  cursor: pointer;
  transition: all .3s;
}
.fechar:hover {
  background-color: #3B5CA7;
  color: #FFCB05;
}

@keyframes show-up {
  from {
    opacity: 0;
  } to {
    opacity: 1;
  }
}

@media (max-width: 400px) {
  h3 {
    width: 90%;
  }
}
</style>
