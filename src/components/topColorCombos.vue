<template>
  <div>
    <ul>
      <li v-for="combo in topCombos">
        <button v-on:click="changeColor(combo.color_one)">
          {{combo.color_one}}        
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'TopColorCombos',
  props: {
    changeColor: Function
  },
  data() {
    return {
      topCombos: []
    }
  },
  created: function() {
    this.fetchTopCombos()
  },
  methods: {
    fetchTopCombos: function() {
      axios.get('https://randoma11y.com/combos/top').then( res => {
        this.topCombos = res.data.slice(0,10).map( combo => {
          combo.color_one = this.ensureSixDigitHex(combo.color_one)
          return combo
        })
      })
    },
    ensureSixDigitHex: function(hexCode) {
      let hashlessCode = hexCode.slice(1)
      if (hashlessCode.length === 6)
        return hexCode

      let sixDigitHex = "#"
      for (var i = 0; i < hashlessCode.length; i++) {
        sixDigitHex += hashlessCode[i] + hashlessCode[i]
      }
      return sixDigitHex
    }
  }
}
</script>

<style>
</style>
