<template>
<div>
  <h1 class="mt-3">Pokemon List</h1>
  <!-- <input type="text" v-model="search" placeholder="Search pokemon..."/> -->
  <div style="display: flex; flex-direction: row; flex-wrap: nowrap; align-items: start;">
    <div class="card-body d-flex flex-row flex-wrap" style="width: 18rem;">
      <div v-for="item in urls" >
        <Pokemon :url="item" @name="name"/>
      </div>
    </div>
    <div class="mr-5 mt-5">
      <FavouriteList :nameToFavourite="nameToFavourite"/>
    </div>
  </div>

</div>

</template>

<script>
import Pokemon from '@/components/Pokemon.vue'
import FavouriteList from '@/components/FavouriteList.vue'

export default {
  name: 'pokemonList',
  components: {
    Pokemon,
    FavouriteList
  },
  data: function() {
      return {
          names: null,
          urls: null,
          search: '',
          nameToFavourite: ''
      };
  },
  methods: {
    name(val) {
      this.nameToFavourite = val
    }
  },
  mounted(){
    const offset = Math.floor(Math.random() * 100)
    fetch(`https://pokeapi.co/api/v2/pokemon?limit=30&offset=${offset}`)
      .then(response => response.json())
      .then(data => {
          this.urls = data.results.map(r => r.url)
          this.names = data.results.map(r => r.name)
      })
  }
}
</script>

<style>
.pokemonBox {
    height: 20em;
    width: 11em;
    background: #E8E8E8;
    border-radius: 25px;
    padding: 25px;
    margin: 30px
  }
.pokemonList {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    padding:10px;
    margin-bottom: 20px;
    width: 18rem;
  }
.container {
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
}
</style>