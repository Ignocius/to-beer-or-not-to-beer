<template>
  <div class="modal d-flex  simple__modal justify-content-center" v-if="isShown">
    <div class="simple__modal__wrapper d-flex flex-column justify-content-between">
      <div class="simple__modal__header d-flex justify-content-between align-items-center">
        <slot name="header" />
        <span class="d-flex justify-content-end align-items-center" @click="onClose">X</span>
      </div>
      <div class="simple__modal__body">
        <slot name="body" />  
      </div>  
      <div class="simple__modal__footar d-flex justify-content-end align-items-center">
        <slot name="footer">
          <button class="close-modal" type="button" @click="onClose"> Close Modal </button>
        </slot>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'SimpleModal',
    props: {
      isShown: {
        type: Boolean,
        default: true
      },
    },
    data() {
      return {
        shown: null
      }
    },
    methods: {
      onClose() {
        this.$emit('close')
      }
    }
  }
</script>

<style lang="scss" scoped>
$gray: #eaeaea;
$height: 50px;
.modal {
  background: #00000059;
  .simple__modal{
    .close-modal{
      cursor: pointer;
    }
    &__wrapper {
      background: #ffffff;
      min-height: 75px;
      margin: 3vw 3vw;
      box-shadow: 5px 8px 5px 4px rgba(0, 0, 0, 0.33);
    }
    &__header {
      min-height: $height;
      background: $gray;
    }
    &__body {
      padding: 0 15px;
    }
    &__footar {
      min-height: $height;
      background: $gray;
      button {
        height: 60%;
      }
    }
  }
}
</style>