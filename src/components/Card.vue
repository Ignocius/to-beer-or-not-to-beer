<template>
  <div>
    <b-card 
      :title="cardData.title"
      :img-src="cardData.image_url"
      img-alt="Image"
      img-top
      tag="article"
      class="mb-2">
    <p class="card-text">
      {{cardData.description}}
    </p>
    <button class="btn btn-primary" type="button" @click="showExtraData = !showExtraData" >Show more</button>
  </b-card>
  </div>
</template>

<script>
  export default {
    name: 'card',
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

    }
  }
</script>

<style lang="scss" scoped>
.card {
  margin-top: 30px;
  -webkit-box-shadow: 9px 10px 5px 0px rgba(0,0,0,0.39);
  -moz-box-shadow: 9px 10px 5px 0px rgba(0,0,0,0.39);
  box-shadow: 9px 10px 5px 0px rgba(0,0,0,0.39);
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