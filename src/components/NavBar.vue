<template>
  <div>
    <search-bar v-bind="defaultField" @input="onChange" />
  </div>
</template>

<script>
import SearchBar from './InputField' 

export default {
  name: 'NavBar',
  components: {
    SearchBar
  },
  props: {
    field: {
      type: Object,
      default: () => {}
    }
  },
  data() {
    return {
      defaultField: {
        id: 'name',
        type: 'text',
        payload_type: 'beer_name',
        value: ''
      }
    }
  },
  methods: {
   onChange($event)  {
     this.defaultField.value = $event.target.value
     const payload = {
       payload_type: this.defaultField.payload_type,
       value: this.defaultField.value
     }
     this.$emit('change', payload)
   }
  },
  created() {
    if(this.field && Object.keys(this.field).length > 0) {
      Object.assign(this.defaultField, this.field)
    }
  }
}
</script>

<style <style lang="scss" scoped>

</style>