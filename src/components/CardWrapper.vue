<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button type="button" @click="fetchBeer">Beer </button>
  </div>
</template>

<script>
const API_URL = 'https://api.punkapi.com/v2/beers'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      loading: false,
      params: {
        abv_gt: 3
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
        const data = await fetch(url)
        console.log(await data.json().catch(e => console.log('An error occured:', e)))
        this.loading = !this.loading
      }
      getData()
    },
  },
}
</script>

<style lang="scss" scoped>
$color: red;

h1 {
  color: $color;
}
</style>
