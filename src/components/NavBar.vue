<template>
  <div class="d-flex navbar__dropdown flex-md-row justify-content-md-center align-items-center justify-content-sm-around">
    <slot />
    <b-dropdown id="ddown-dropup" dropup text="Change Search" class="navbar__dropdown__btn">
      <b-dropdown-item v-for="dropItem in dropdownMock" :key="dropItem.name" @click="changeField(dropItem)">{{dropItem.name}}</b-dropdown-item>
    </b-dropdown>
    <search-bar v-bind="reAssignField" @input="onChange" />
  </div>
</template>

<script>
import SearchBar from './InputField' 
import moment from 'moment'
import { debounce } from 'lodash'

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
      },
      dropdownMock: [
        {
          name: 'Add Beer Name',
          payload_type: 'beer_name',
          type: 'text'
        },
        {
          name: 'Add Beer Yeast',
          payload_type: 'yeast',
          type: 'text'
        },
        {
          name: 'Beer Brewed Before',
          payload_type: 'brewed_before',
          type: 'month',
          format: 'en'
        },
      ]
    }
  },
  methods: {
    onChange: debounce( 
      function ($event) {
        let value
        if(this.reAssignField.type === 'month' || this.reAssignField.type === 'date') {
          value = moment($event.target.value).format('MM-YYYY')
        }
        this.defaultField.value = value ? value :  $event.target.value
        const payload = {
          payload_type: this.defaultField.payload_type,
          value: this.defaultField.value
        }
        this.$emit('change', payload)
    }, 1500),
    changeField(newField) {
     this.reAssignField = newField
    }
  },
  computed: {
    reAssignField: {
      get() {
        return this.defaultField
      }, 
      set(newVal) {
        if(!newVal) return
        Object.assign(this.defaultField, newVal)
      }
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
.navbar__dropdown {
  width: 100vw;
  overflow: hidden;
  margin-left: -15vw;
  z-index: 0;
  &__btn {
    color: #818181;
    background-color: #fffefe;
    border-color: #c1c1c1;
  }
}


@media only screen and (max-width: 600px) {
  .navbar__dropdown {
    flex-direction: column;
  }
  .navbar_contianer {
    max-height: 150px
  }
}
</style>