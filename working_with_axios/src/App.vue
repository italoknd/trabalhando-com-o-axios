<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>Fazendo requisições HTTP com o AXIOS</h1>
    <div>{{pokemons}}</div>
    <ul>
      <li v-for="pokemon in pokemons" :key="pokemon.id">{{pokemon.name}}</li>
    </ul>
  </div>
</template>

<script>
import {defineComponent, onMounted, ref} from 'vue'
import api from './services/api'

export default defineComponent({
  name: 'App',
  setup() {
    const pokemons = ref([]);
    console.log(pokemons);

    const fetchPokemons = () =>
      api
        .get('/pokemon?limit=20')
        .then((response) => {
          pokemons.value = response.data.results,
          console.log(response)
        })
        .catch(err => {
          console.log(err)
        })

    onMounted(fetchPokemons);
    
    return {pokemons};
  },
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

ul{
margin-top:80px;
}

li{
  text-align: left;
}
</style>
