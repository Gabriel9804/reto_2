<template lang="html">
  <div class="header">
      <img class="header_logo" src="../assets/logo_FractalUp.png" alt="logo">
  </div>
</template>

<script>
export default {
    name: 'FuHeader',
}
</script>

<style lang="css" scoped>
.header{
    width: 100%;
    height: 70px;
    background: #2196F3;
    display: flex;
    justify-content: center;
    align-items: center;
}
.header_logo{
    width: 154px;
    height: 42px;
}
</style>
