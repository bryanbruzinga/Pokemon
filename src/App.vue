<template>
  <div id="app">
      <p>{{dados.id}}</p>
      <img :src="dados.sprites.front_default" :alt="dados.name">
      <p>{{dados.name}}</p>
      <p>{{dados.types}}</p>      
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      dados: {}
    }
  },
  methods: {
    puxarApi() {
      fetch('https://pokeapi.co/api/v2/pokemon/1')
      .then(r => r.json())
      .then(json => {
        this.dados = json
      })
    }
  },
  created() {
    this.puxarApi()
  }
}
</script>

<style>

* {
  box-sizing: border-box;
}
body,
ul,
li,
h1,
h2,
p {
  margin: 0;
  padding: 0;
}
ul {
  list-style: none;
}
body {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  color: #345;
}
a {
  color: #345;
  text-decoration: none;
}
img {
  max-width: 100%;
  display: block;
}

</style>
