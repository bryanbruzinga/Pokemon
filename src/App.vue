<template>
  <div id="app">
        <Pokemon />
  </div>
</template>

<script>

import Pokemon from "@/components/Pokemon.vue"

export default {
  name: 'App',
  components: {
    Pokemon
  }
}

</script>

<style>

* {
  box-sizing: border-box;
  text-transform: capitalize;
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
  background: url('./assets/background.jpeg');
}
a {
  color: #345;
  text-decoration: none;
}
img {
  height: 100px;
  width: 100px;
  display: block;
}

</style>
