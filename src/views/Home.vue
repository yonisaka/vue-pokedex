<template>
  <div class="home">
    <h2 class="mt-5">Pokedex</h2>
    <PokemonCard/>
  </div>
</template>

<script>
// @ is an alias to /src
import 'bootstrap/dist/css/bootstrap.css'
import PokemonCard from '@/components/PokemonCard.vue'


export default {
  name: 'Home',
  components: {
    PokemonCard
  }
}
</script>
