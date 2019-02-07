<template>
  <div>
    <input v-bind="$props" ref="input"  v-on="$listeners" @click="active = !active" :class="{active: active}" :placeholder="placeHolder" class="search__field" />
  </div>
</template>

<script>
  export default {
    name: 'SearchBar',
    props: ['type', 'id', 'name'],
    data() {
      return {
        active: false,
        placeHolder: 'Search here'
      }
    },
    methods: {
      clickCheck() {
        console.log('call')
        window.addEventListener('click', (event)=>{
          const target = event.target
          if(target !== this.$refs.input) {
            this.active = false
          }
        })
      },
    },
    mounted() {
      this.clickCheck()
    }
  }
</script>

<style lang="scss" scoped>
.search__field {
  font-family: 'Caveat', cursive;
  width: 25vw;
  transition: width 2s;
  border: 0;
  border-bottom: 3px solid #c1c1c1;
  outline: none;
  text-align: center;
  font-size: calc(16px + 5 * ((100vw - 320px) / 680));
  &:placeholder-shown {
    color: gray;
    font-family: 'Caveat', cursive;
  }
  &.active {
    width: 50vw;
    transition: width 2s;
  }
}
</style>