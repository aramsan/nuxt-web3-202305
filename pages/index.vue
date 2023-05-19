<template>
  <Tutorial/>
</template>

<script>
export default {
  name: 'IndexPage',
  mounted() {
    console.log('Current Block Number')
    this.$web3.eth.getBlockNumber().then(console.log)
  }
}
</script>
