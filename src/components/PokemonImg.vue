<template>
    <img :src="this.urlImg"/>
</template>

<script>

export default {
  props: ["urlImg"],
  name: 'pokemonImg',

}
</script>