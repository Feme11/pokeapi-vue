<template>
  <div id="app">
    <div>
      <input type="text" v-model="name" @keyup.enter="busqueda_pokemon"><button @click="busqueda_pokemon" >Buscar</button>
    </div>
    <div>
      <img :src="datos.sprites.front_default" alt=""/>
      <h3> {{this.datos.name}} </h3>
    </div>
    <div>
      <h4>Habilidades</h4>
      <ul>
        <li v-for="(habilidad, index) in get_habilidades" :key="index"> {{habilidad.ability.name}} </li>
      </ul>
    </div>
    <div>
      <h4>Movimientos</h4>
      <ul>
        <li v-for="(move, index) in get_moves" :key="index"> {{move.move.name}} </li>
      </ul>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      name: "",
      datos: []
    }
  },
  methods: {
    busqueda_pokemon() {
      fetch("https://pokeapi.co/api/v2/pokemon/" + this.name)
      .then(res => res.json())
      .then(data => {
        (this.datos = data)
      });
    }
  },
  created(){
    fetch("https://pokeapi.co/api/v2/pokemon/pikachu" + this.name)
    .then(res => res.json())
    .then(data => {
      this.datos = data;
    });
  },
  computed: {
    get_picture(){
      if(this.datos.sprites){
        return this.datos.sprites.front_default
      }else{
        return ''
      }
    },
    get_name(){
      return this.datos.name
    },
    get_habilidades(){
      return this.datos.abilities
    },
    get_moves(){
      return this.datos.moves
    },
    
  }
}
</script>

<style>

</style>
