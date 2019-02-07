<template>
  <div class="d-flex navbar_contianer justify-content-center align-items-center">
    <slot />
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

<style lang="scss" scoped>
.navbar_contianer {
  width: 100vw;
      background: linear-gradient(to bottom, rgb(255, 255, 255) 0%, rgb(255, 254, 254) 39%, rgb(255, 255, 255) 75%, rgba(255, 253, 253, 0.45) 94%, rgba(228, 227, 225, 0.69) 100%);
  overflow: hidden;
  margin-left: -15vw;
  z-index: 0;
}

@media only screen and (max-width: 600px) {
  .navbar_contianer {
    max-height: 150px
  }
}
</style>