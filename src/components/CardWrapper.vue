<template>
  <div class="card-wrapper contianer">
    <nav class="d-flex">      
      <div class="beer-logo-container d-flex"> 
        <img alt="Beeeeeer" class="beer-logo" src="../assets/glass.png">
      </div>
      <nav-bar @change="onChange" >
      </nav-bar>
    </nav>
    <section class="row wrapper mr-5 ml-5">
      <loader :loading="loading" />
      <div v-for="beer in beerBank" :key="beer.anme" class="col-sm-6 col-md-3 d-flex justify-content-center"> 
        <card :card-data="beer"/>
      </div>
    </section>
  </div>
</template>

<script>
import ndjsonStream from 'can-ndjson-stream'
import Card from './Card'
import Loader from './Loader'
import NavBar from './NavBar'
const API_URL = 'https://api.punkapi.com/v2/beers'

export default {
  name: 'CardWrapper',
  components: {
    Card,
    Loader,
    NavBar
  },
  props: {
    url: String
  },
  data() {
    return {
      loading: false,
      beerData: [],
      params: {
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
    onChange({payload_type, value}) {
      if(value) {
        Object.assign(this.params, {[payload_type]: value})
        this.fetchBeer()
      }
    }
  },
  computed: {
    beerBank: {
      get() {
        return this.beerData
      },
      set(newVal) {
        if(newVal && newVal instanceof Array) {
          this.beerData = newVal.map(item =>  item)
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@mixin Gradient {
  background: linear-gradient(-45deg, #EE7752, #E73C7E, #23A6D5, #23D5AB);
}

.card-wrapper {
  font-family: 'Montserrat', sans-serif;
  background: #e4e3e1;
  .wrapper {
    position: relative;
  }
  .beer-logo-container {
    width: 20vw;
    min-width: 100px;
    height: 35vh;
    border-top-right-radius: 0;
    border-bottom-right-radius: 83%;
    overflow: hidden;
    //background: white;
    @include Gradient;
    background-size: 400% 400%;
    -webkit-animation: Gradient 15s ease infinite;
    -moz-animation: Gradient 15s ease infinite;
    animation: Gradient 15s ease infinite;
    box-shadow: 9px 2px 12px 0px rgba(0, 0, 0, 0.39);
    z-index: 1;
    .beer-logo {
      vertical-align: middle;
      border-style: none;
      width: 100%;
      background: black;
      overflow: hidden;
      border-bottom-right-radius: 83%;
    }
  }
}

@keyframes Gradient {
	0% {
		background-position: 0% 50%
	}
	50% {
		background-position: 100% 50%
	}
	100% {
		background-position: 0% 50%
	}
}

@media only screen and (max-width: 600px) {
  nav {
    .beer-logo-container {
      max-height: 150px;
    }
  }
}
</style>
