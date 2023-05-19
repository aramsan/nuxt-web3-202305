<template>
  <div>
    <p>
      <input
        type="text"
        v-model="inputNumber"
        placeholder="input number"
      >
      <button
        @click="setNumber()"
      >
        Set Number to contract
      </button>
      </p>
      <p>
      <button
        @click="getNumber()"
      >
        Get Number from contract
      </button>
        Number:{{number}}
    </p>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      number: 0, // コントラクトから取得する数値
      inputNumber: 0 // フォームから入力された数値
    }
  },
  methods: {
    getNumber: async function() {
      let ret = await this.$contract.methods.get().call() // コントラクトからの読み込み部分
      this.number = ret // フロントへ反映
    },
      setNumber: async function() {
      let accounts = await this.$web3.eth.getAccounts() // MetaMask で使っているアカウントの取得
      let account = accounts[0]
      let ret = await this.$contract.methods.set(this.inputNumber).send({from: account}) // コントラクトへの書き込み部分
    },
  },
  mounted() {
    console.log('Current Block Number')
    this.$web3.eth.getBlockNumber().then(console.log)
  }
}
</script>
