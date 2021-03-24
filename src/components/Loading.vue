<template>
  <div class="container">
    <div class="pokebola" v-if="loading">
      <div class="pokebola-botao"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Loading",
  data() {
    return {
      loading: false,
    };
  },
  methods: {
     loadingOn() {
      this.loading = true;
    },
    loadingOff() {
      this.loading = false;
    }
  }
};
</script>

<style scoped>
.container {
  position: absolute;
  height: 100vh;
  width: 100%;
  top: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  display: none;
  animation: show-up 0.3s linear;
}

@keyframes show-up {
  to {
    opacity: 1;
    display: block;
  }
}
.pokebola {
  position: relative;
  width: 150px;
  height: 150px;
  background-color: #fff;
  border: 5px solid #000;
  border-radius: 50%;
  box-shadow: inset -10px 10px 0 10px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  animation: gira 3s infinite ease-out;
  z-index: 20;
}
.pokebola::before,
.pokebola::after {
  content: "";
  position: absolute;
}
.pokebola:before {
  background-color: #ef4036;
  width: 100%;
  height: 50%;
}
.pokebola:after {
  top: calc(50% - 10px);
  width: 100%;
  height: 20px;
  background-color: #000;
}
.pokebola-botao {
  width: 50px;
  height: 50px;
  background-color: #fff;
  border: 10px solid #000;
  border-radius: 50%;
  position: absolute;
  top: calc(50% - 25px);
  left: calc(50% - 25px);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}
.pokebola-botao::before {
  content: "";
  position: absolute;
  width: 20px;
  height: 20px;
  background-color: #fff;
  border: 3px solid #000;
  border-radius: 50%;
  z-index: 10;
}

@keyframes gira {
  0% {
    transform: rotate(-45deg);
  }
  50% {
    transform: rotate(45deg);
  }
  100% {
    transform: rotate(-45deg);
  }
}
</style>
