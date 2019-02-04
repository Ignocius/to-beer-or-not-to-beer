<template>
  <div class="loader-wrapper" v-if="loading">
    <div class="loading wave">
      Loading
    </div>
    <slot />
  </div>
</template>

<script>
  export default {
    name: "loader",
    props: {
      loading: {
        type: Boolean,
        default: false
      }
    }
  }
</script>

<style lang="scss" scoped>
$background-color:#141414;
.loader-wrapper {
  width:100%;
  height:100%;
  z-index: 3;
  position: sticky;
  top: 0;
  .loading{
    text-transform:uppercase;
    font-family: 'Cabin Condensed', sans-serif;
    font-weight:bold;
    font-size:100pt;
    text-align:center;
    height:120px;
    line-height:110px;
    vertical-align:bottom;
    position:absolute;
    left:0;
    right:0;
    top:100px;
    bottom:0;
    display:block;
  }
  @keyframes wave-animation{
    0%{background-position:0 bottom};
    100%{background-position:200px bottom};
  }
  @keyframes loading-animation{
    0%{background-size:200px 0px};
    100%{background-size:200px 200px};
  }
  .wave{
    background-image:url('http://i66.tinypic.com/optxd3.png');
    //@include background-clip(text);
    color: rgba(2, 2, 2, 0.31);
    text-shadow:0px 0px rgba(255,255,255,0.06);
    animation:wave-animation 1s infinite linear, loading-animation 10s infinite linear alternate;
    background-size:200px 100px;
    background-repeat:repeat-x;
    opacity:1;
  }
}

</style>