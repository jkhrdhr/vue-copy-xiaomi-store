<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  name: 'app',
  created () {
    this.getUserMsg()
    this.getCard()
  },
  provide () {
    return {
      getUserMsg: this.getUserMsg,
      getCard: this.getCard
    }
  },
  methods: {
    ...mapActions(['modCardNum', 'modUserMsg']),
    async getUserMsg () {
      const res = await this.axios.get('/user')
      if (res) { this.modUserMsg(res) } else {
        this.modUserMsg({})
      }
    },
    async getCard () {
      const res = await this.axios.get('/carts/products/sum')
      this.modCardNum(res)
    }
  }
}
</script>

<style lang="less">
@import url(./assets/less/reset.less);
@import url(./assets/less/config.less);
</style>
