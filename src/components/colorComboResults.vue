<template>
  <div className="color-combos">
    <h3>Combos</h3>
    <ul v-if="!loading">
      <li v-for="combo in combos">
        {{getComboColor(combo)}}
      </li>
    </ul>
    <div v-else>loading</div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'ColorComboResults',
  props: {
    color: String
  },
  data() {
    return {
      combos: [],
      loading: false
    }
  },
  methods: {
    getComboColor: function(combo) {
      return this.color === combo.color_one ? combo.color_two : combo.color_one
    },
    fetchCombos: function(color) {
      this.loading = true
      axios.get('https://randoma11y.com/combos', {
        params: { hex: color }
      }).then( res => {
        this.combos = res.data
        this.loading = false
      })
    }
  },
  watch: {
    color: function(newColor) {
      this.fetchCombos(newColor)
    }
  }
}
</script>

<style>
</style>
