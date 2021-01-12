<template>
  <div id="nav-bar">
    <div class="left">
      <slot name="left"></slot>
    </div>
    <div class="center">
      <slot name="center"></slot>
    </div>
    <div class="right">
      <slot name="right"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "NavBar"
}
</script>

<style scoped>
  #nav-bar{
    height: 49px;
    display: flex;
  }
  #nav-bar div{
    flex: 1;
    text-align: center;
    line-height: 49px;
  }
</style>