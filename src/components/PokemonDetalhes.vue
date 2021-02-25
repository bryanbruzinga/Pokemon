<template>
  <div class="detail">
    <div class="detail-view" v-if="show">
      <div v-if="pokemon" class="image">
        <img :src="imgUrl + pokemon.id + '.png'" alt="pokemon.name" />
      </div>
      <div v-if="pokemon" class="data">
        <h2>{{ pokemon.name }}</h2>
        <div class="property">
          <div class="left">Experiência Base</div>
          <div class="right">{{ pokemon.base_experience }} XP</div>
        </div>
        <div class="property">
          <div class="left">Altura</div>
          <div class="right">{{ pokemon.height / 10 }} m</div>
        </div>
        <div class="property">
          <div class="left">Peso</div>
          <div class="right">{{ pokemon.weight / 10 }} kg</div>
        </div>
        <h3>Tipo</h3>
        <div class="types">
          <div
            class="type"
            v-for="(tipo, index) in pokemon.types"
            :key="'tipo' + index"
          >
            {{ tipo.type.name }}
          </div>
        </div>
        <h3>Habilidades</h3>
        <div class="abilities">
          <div
            class="ability"
            v-for="(habilidade, index) in pokemon.abilities"
            :key="'habilidade' + index"
          >
            {{ habilidade.ability.name }}
          </div>
        </div>
      </div>
      <h2 v-else>O Pokemon não foi encontrado</h2>
      <button class="close" @click="fecharDetalhes">Fechar</button>
    </div>
    <i v-else class="fas fa-spinner fa-spin"></i>
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
.detail {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  position: fixed;
  top: 0;
  left: 0;
  padding: 90px 10px 10px;
  width: calc(100% - 20px);
  height: calc(100vh - 20px);
  background: rgba(255, 255, 255, 0.7);
}
.detail-view {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  position: relative;
  width: 100%;
  max-width: 510px;
  padding: 50px 0 0;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}

.image {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: -60px;
  width: 120px;
  height: 120px;
  background-color: #333;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}

h2 {
  text-transform: capitalize;
}
.data {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  flex-direction: column;
  width: 100%;
  margin-bottom: 40px;
}
.property {
  width: 90%;
  max-width: 400px;
  border-bottom: 1px solid #ccc;
  margin-bottom: 10px;
}
h3 {
  width: 90%;
  max-width: 400px;
  border-bottom: 1px solid #ccc;
}
.types,
.abilities {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  width: 90%;
  max-width: 400px;
}
.type,
.ability {
  margin: 0 10px 10px 0;
  padding: 5px 10px;
  border-radius: 20px;
  color: #fff;
  font-size: 1rem;
  letter-spacing: 2px;
  text-transform: capitalize;
  word-wrap: none;
  word-break: keep-all;
}
.type {
  background-color: #0a2e50;
}
.ability {
  background-color: #c73015;
}
.close {
  outline: none;
  border: none;
  border-radius: 5px;
  background-color: #333;
  color: #efefef;
  padding: 10px 20px;
  margin-bottom: 20px;
  font-size: 1.2rem;
  cursor: pointer;
}
i {
  font-size: 2rem;
  color: #efefef;
}
</style>
