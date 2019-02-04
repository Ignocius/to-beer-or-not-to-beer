<template>
  <div class="card-wrapper">
    <h1>{{ msg }}</h1>
    <button type="button" @click="fetchBeer">Beer </button>
    <section class="row">
      <div v-for="beer in beerBank" :key="beer.anme" class="col-sm-6 col-md-3 d-flex justify-content-center"> 
        <card :card-data="beer"/>
      </div>
    </section>
  </div>
</template>

<script>
import ndjsonStream from 'can-ndjson-stream'
import Card from './Card'
const API_URL = 'https://api.punkapi.com/v2/beers'

export default {
  name: 'HelloWorld',
  components: {
    Card
  },
  props: {
    msg: String
  },
  data() {
    return {
      loading: false,
      beerData: [],
      params: {
        //abv_gt: 3
      }
    }
  },
  methods: {
    fetchBeer() {
      const getData = async () => {
        this.loading = !this.loading
        const url = new URL(API_URL)
        if(Object.keys(this.params).length > 0) {
           url.search = new URLSearchParams(this.params)
        }
        const response = await fetch(url)
        const reader = ndjsonStream(response.body).getReader()
        let result
        while (!result || !result.done) {
          result = await reader.read()
          if(result.value) {
            this.beerBank = result.value
          }
        }
        this.loading = !this.loading
      }
      getData()
    },
  },
  computed: {
    beerBank: {
      get() {
        return this.beerData
      },
      set(newVal) {
        this.beerData = newVal.map(item =>  item)
      }
    }
  }
}
</script>

<style lang="scss" scoped>
$color: red;
.card-wrapper {
  background: #e4e3e1;
  h1 {
    color: $color;
  }
}

</style>
