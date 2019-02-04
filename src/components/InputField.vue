<template>
  <div>
    <input v-bind="$props" v-on="$listeners" />
  </div>
</template>

<script>
  export default {
    name: 'SearchBar',
    props: ['type', 'id', 'name']
  }
</script>

<style scoped>

</style>