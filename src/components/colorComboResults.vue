<template>
  <div className="color-combos">
    <h3>Combos</h3>
    <ul>
      <li v-for="combo in combos">
        {{getComboColor(combo)}}
      </li>
    </ul>
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
      combos: []
    }
  },
  methods: {
    getComboColor: function(combo) {
      return this.color === combo.color_one ? combo.color_two : combo.color_one
    }
  },
  watch: {
    color: function(newColor) {
      var self = this
      axios.get('https://randoma11y.com/combos', {
        params: { hex: newColor }
      }).then( res => self.combos = res.data)
    }
  }
}
</script>

<style>
</style>
