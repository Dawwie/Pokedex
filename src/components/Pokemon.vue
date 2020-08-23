<template>
<div>

  <div class="pokemonList" style="padding:10px; margin-bottom: 20px">
    <div class="card bg-light p-2 d-flex flex-column justify-content-center" style="width:14rem">
        <div><PokemonImg :urlImg="this.img" style="height: 120px; width: 120px"/></div>
        <p style="text-transform: capitalize"><strong>{{name}}</strong></p>
        <p>#{{this.id}}</p>
        <div class="d-flex flex-row justify-content-center">
            <span class="badge badge-warning px-3 py-2 m-2" style="color:white">{{type}}</span>
            <span class="badge badge-warning px-3 py-2 m-2" style="color:white">{{ability}}</span>
        </div>
        <div class="d-flex flex-column justify-content-center">
            <router-link :to="{path: `details/${this.id}`, query: { img: this.img, weight: this.weight, height: this.height }}">
                <button type="button" class="btn btn-light m-1">Details</button>
            </router-link>
            <div><button type="button" class="btn btn-light m-1" @click="sendName()">Toggle favuorite</button></div>
        </div>
    </div>
  </div>
</div>

</template>

<script>
import Pokemon from '@/components/Pokemon.vue'
import PokemonImg from '@/components/PokemonImg.vue'

export default {
  props: ["url"],
  name: 'PokemonList',
  components: {
    Pokemon,
    PokemonImg
  },
  data: function() {
      return {
          id: null,
          name: null,
          ability: null,
          type: null,
          img: null,
          weight: null,
          height: null,
      };
    },

    methods: {
      getPokemonNames() {
        fetch(this.url)
          .then(response => response.json())
          .then(data => {
              this.id = data.id
              this.name = data.name
              this.type = data.types[0].type.name
              this.ability = data.abilities[0].ability.name
              this.img = data.sprites.front_shiny
              this.weight = data.weight
              this.height = data.height
          })
      },
      sendName() {
          this.$emit("name", this.name)
      }
    },
    mounted() {
        this.getPokemonNames()
    }
}
</script>

