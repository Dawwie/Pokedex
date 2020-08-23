<template>
<div >
    <h1 class="py-4">Pokemon Details</h1>
    <div class="d-flex flex-row justify-content-center">
        <div class="card bg-light  p-3 d-flex flex-column justify-content-center" style="width: 350px">
            <h2 style="text-transform: uppercase">{{name}}</h2>
            <div>
                <pokemonImg :urlImg="img" style="width: 200px; height:200px"></pokemonImg>
            </div>
            <div style="padding: 20px">
                <hr >
                    <p style="font-style: italic; font-size: 15px">{{desc}}</p>
                <hr >
            </div>
            <p style="font-weight: bold; font-size: 13px">Weight: {{weight}} lbs.</p>
            <p style="font-weight: bold; font-size: 13px">Height: {{height}}'</p>
        </div>
    </div>
</div>

</template>

<script>

import PokemonImg from '@/components/PokemonImg.vue'

export default {
  name: 'PokemonDetails',
    components: {
    PokemonImg
  },

  data: function() {
      return {
          id: null,
          name: null,
          img: null,
          desc: null,
          weight: null,
          height: null
      };
    },
    methods: {
      getPokemonNames() {
        fetch(`https://pokeapi.co/api/v2/pokemon-species/${this.id}`)
          .then(response => response.json())
          .then(data => {
              this.name = data.name
              this.desc = data.flavor_text_entries[0].flavor_text
          })
      },
    },
    created() {
        this.id = this.$route.params.id
        this.img = this.$route.query.img
        this.weight = this.$route.query.weight
        this.height = this.$route.query.height
    },
    mounted() {
        this.getPokemonNames()
    }
}
</script>

