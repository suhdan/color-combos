<template>
  <div class="color-combos">
    <h3>Combos</h3>
    <ul v-if="!loading">
      <li :key="combo.id" v-for="combo in combos">
        <div 
          class="combo-one"
          v-bind:style="{background: getComboColor(combo), color: color}" 
        >
          {{color}}
        </div>
        <div 
          class="combo-two"
          v-bind:style="{background: color, color: getComboColor(combo)}" 
        >
          {{getComboColor(combo)}}
        </div>
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

<style lang="scss">
.color-combos {
  h3 {
    text-align: center;
    margin-bottom: 15px;
  }
  li {
    display: flex;
    justify-content: center;
    width: 75%;
    margin: 0 auto;

    div {
      padding: 15px 10px;
      flex: 1;
      text-align: center;
    }
  }
}
</style>
