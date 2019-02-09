<template>
  <div class="modal d-flex  simple__modal justify-content-center" v-if="isShown">
    <div class="simple__modal__wrapper d-flex flex-column justify-content-between" r :style="height">
      <div class="simple__modal__header d-flex justify-content-between align-items-center">
        <slot name="header" />
        <span class="d-flex justify-content-center align-items-center close-modal" @click="onClose">X</span>
      </div>
      <div class="simple__modal__body">
        <slot name="body" />  
      </div>  
      <div class="simple__modal__footer d-flex justify-content-end align-items-center">
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
      styleOptions: {
        type: Object,
        default: () => {}
      }
    },
    data() {
      return {
        shown: null,
        height: 'auto',
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
  .close-modal{
    cursor: pointer;
  }
  h5 {
    margin-left: 5%;
  }
  .simple__modal{
    &__wrapper {
      background: #ffffff;
      min-height: 75px;
      margin: 3vw 3vw;
      box-shadow: 5px 8px 5px 4px rgba(0, 0, 0, 0.33);
    }
    &__header {
      min-height: $height;
      background: $gray;
      span {
        width: 30px;
        height: 100%;
      }
    }
    &__body {
      padding: 0 15px;
    }
    &__footer {
      min-height: $height;
      background: $gray;
      button {
        height: 60%;
      }
    }
  }
}
</style>