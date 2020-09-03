<template>
  <div class="pokemon-card">
    <div class="container">
      <div class="row mt-5">
        <div v-for="poke in dataPokemon" :key="poke.name" class="col-lg-3 col-md-6 col-sm-11 mb-3">
          <div class="card shadow-sm border-0">
            <div class="card-body">
              <img v-bind:src="poke.imgPokemon" v-bind:alt="pokemon" class="img rounded" style="max-height:100px;"/>
              <!-- <a href={{poke.imgPokemon}}>{{poke.imgPokemon}}</a> -->
              <h5 class="mt-3 text-uppercase"> {{ poke.name }} </h5>
              <p class="text-uppercase">{{ poke.tipePokemon }}</p>
            </div>
          </div>
        </div>
      </div>
      <div class="footer mt-3 mb-5">
        <div class="mx-auto">
          <button class=" btn btn-secondary btn-sm mr-3" @click="load(previous)">Previous</button>
          <button class=" btn btn-secondary btn-sm" @click="load(next)">Next</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'PokemonCard',
  data(){
    return{
      dataPokemon: [],
      next: '',
      previous: '',
      url: 'https://pokeapi.co/api/v2/pokemon'
    }
  },
  mounted(){
    this.load(this.url)
  },
  methods: {
    load(url){
          axios.get(url).then(res => {
          this.next = res.data.next;
          this.previous = res.data.previous;
          console.log(this.next)
          this.dataPokemon = res.data.results
          this.dataPokemon.forEach(item => {
            axios.get(item.url).then(res => {
                item.imgPokemon = 'https://pokeres.bastionbot.org/images/pokemon/' + res.data.id + '.png'
                if (res.data.types.length < 2) {
                  const datas = res.data.types[0].type.name;
                  item.tipePokemon = datas;
                } else {
                  const datas0 = res.data.types[0].type.name;
                  const datas1 = res.data.types[1].type.name;
                  item.tipePokemon = datas0 + ' - ' + datas1;
                }
            })
          });
      }).catch ((err) => {
          console.log(err);      
      })
    }
  }
}
</script>
