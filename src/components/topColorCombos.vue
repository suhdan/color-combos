<template>
  <div>
    <ul>
      <li v-for="combo in topCombos" v-on:click="changeColor(combo.color_one)">
        {{combo.color_one}}        
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
    axios.get('https://randoma11y.com/combos/top').then( res => {
      this.topCombos = res.data.slice(0,10)
    })
  }
}
</script>

<style>
</style>
