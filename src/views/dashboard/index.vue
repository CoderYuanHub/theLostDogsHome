<template>
  <div class="dashboard-container">
    <div class="dashboard-text">浪浪之家欢迎 {{ name }}</div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'Dashboard',
  computed: {
    ...mapGetters([
      'name'
    ])
  }
}
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
    /*background: url("../../assets/index/index.jpg") no-repeat;*/
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
</style>
