<template>
  <div class="detalhes">
    <div class="detalhes-view" v-if="show">
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
            class="tipo"
            v-for="(tipo, index) in pokemon.types"
            :key="'tipo' + index"
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
  animation: show-up .8s;
}
.detalhes-view {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  position: relative;
  width: 100%;
  max-width: 500px;
  padding: 50px 0 0;
  background-color: #fff;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
}

.imagem {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: -60px;
  width: 100px;
  height: 100px;
  background-color: #333;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: 0 10px 10px rgba(0, 0, 0, 0.2);
}

h2 {
  margin-bottom: 20px;
}
.data {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  flex-direction: column;
  width: 100%;
  margin-bottom: 2rem;
}
.propriedades {
  width: 90%;
  max-width: 400px;
  border-bottom: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  margin-bottom: 1.5rem;
}
h3 {
  width: 90%;
  max-width: 400px;
  border-bottom: 1px solid #ccc;
}
.tipos,
.habilidades {
  display: flex;
  justify-content: center;
  width: 90%;
  max-width: 400px;
}
.tipo,
.habilidade {
  margin-right: 1rem;
  padding: 0.5rem;
  border-radius: 20px;
  color: #fff;
  font-size: 1.125rem;
}
.tipo {
  background-color: #0a2e50;
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
</style>
