<template>
  <div>
    <h2>Most Popular</h2>
    <ul v-if="!loading">
      <li :key="combo.id" v-for="combo in topCombos">
        <button 
          v-bind:style="{background: combo.color_two, color: combo.color_one}" 
          v-on:click="changeColor(combo.color_one)"
        >
          {{combo.color_one}}        
        </button>
        <button
          v-bind:style="{background: combo.color_one, color: combo.color_two}" 
          v-on:click="changeColor(combo.color_two)"
        >
          {{combo.color_two}}        
        </button>
      </li>
    </ul>
    <div v-else>loading</div>
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
      topCombos: [],
      loading: true
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
        this.loading = false
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
