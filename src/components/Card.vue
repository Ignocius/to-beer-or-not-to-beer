<template>
  <div>
    <b-card 
      :title="cardData.name"
      :img-src="cardData.image_url"
      img-alt="Image"
      img-top
      tag="article"
      class="mb-2">
    <p class="card-text">
      {{cardData.description}}
    </p>
    <button class="btn btn-primary" type="button" @click="showExtraData = !showExtraData" >Show more</button>
    <simple-modal :is-shown="showExtraData" @close="onClose"> 
      <slot slot="header">
        <h5>{{cardData.name}}</h5>
      </slot>
      <slot slot="body">
        <p>
          {{cardData.brewers_tips}}
        </p>
        <span>{{cardData.contributed_by}} </span>
        <div class="progress">
          <label>Attenuation level</label>
          <div class="progress-bar" role="progressbar" :style="`width: ${cardData.attenuation_level}%`" :aria-valuenow="cardData.attenuation_level" aria-valuemin="0" aria-valuemax="100"></div>
        </div>
        <b-table striped hover :items="[{attenuation_level: cardData.attenuation_level, ebc: cardData.ebc, }]"></b-table>
        <b-table striped hover :items="cardData.ingredients.malt"></b-table>
      </slot>
    </simple-modal>
  </b-card>
  </div>
</template>

<script>
import SimpleModal from './SimpleModal'
export default {
  name: 'card',
  components: {
    SimpleModal
  },
  props: {
    cardData: {
      type: Object,
      default: () => {}
    },
  },
  data() {
    return {
      showExtraData: false
    }
  },
  methods: {
    onClose() {
      this.showExtraData = false
    }
  }
}
</script>

<style lang="scss" scoped>
.card {
  margin-top: 30px;
  -webkit-box-shadow: 9px 10px 5px 0px rgba(0,0,0,0.39);
  -moz-box-shadow: 9px 10px 5px 0px rgba(0,0,0,0.39);
  box-shadow: 9px 10px 5px 0px rgba(0,0,0,0.39);
  .card-title {
    font-family: 'Caveat', cursive;
    border-bottom: 1px solid #8080804a;
  }
  .card-img-top {
    max-height: 200px;
    object-fit: contain;
    transition: all .4s ease-in-out;
    background:#2b2a2a4a;
    &:hover {
      transform: scale(1.3);
      background: transparent
    }
  }
}
</style>