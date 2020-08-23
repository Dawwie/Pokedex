<template>
    <div class="card text-white bg-warning" style="width:20rem">
        <div class="card-header">Favourite List</div>
        <div style="display:flex; flex-direction: column; justify-content: center">
            <div v-for="name in names" class="pt-2">
                <p class="card-title" style="text-transform: capitalize">{{name}}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  props: ['nameToFavourite'],
  name: 'FavouriteList',
  data: function() {
      return {
        names: []
      };
    },
    watch: {
        nameToFavourite(val) {
            if(!(this.names.includes(val))) this.names.push(val)
        }
    }
}
</script>
