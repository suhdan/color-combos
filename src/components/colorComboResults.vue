<template>
  <div class="color-combos">
    <h2>Combos</h2>
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
    <div v-else>
      <div class='rainbow-wheel'></div>
    </div>
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
  h2 {
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

  .rainbow-wheel {
    margin: 0 auto;
    width: 2em; 
    height: 2em;
    opacity: 0.9;
    border-radius: 50%;
    background: 
      linear-gradient(36deg, #272b66 42.34%, transparent 42.34%) 0 0,
      linear-gradient(72deg, #2d559f 75.48%, transparent 75.48%) 0 0,
      linear-gradient(-36deg, #9ac147 42.34%, transparent 42.34%) 100% 0,
      linear-gradient(-72deg, #639b47 75.48%, transparent 75.48%) 100% 0, 
      linear-gradient(36deg, transparent 57.66%, #e1e23b 57.66%) 100% 100%,
      linear-gradient(72deg, transparent 24.52%, #f7941e 24.52%) 100% 100%,
      linear-gradient(-36deg, transparent 57.66%, #662a6c 57.66%) 0 100%,
      linear-gradient(-72deg, transparent 24.52%, #9a1d34 24.52%) 0 100%, 
      #43a1cd linear-gradient(#ba3e2e, #ba3e2e) 50% 100%;
    background-repeat: no-repeat;
    background-size: 50% 50%;
    animation: spin 1.5s linear forwards infinite
  }
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}
</style>
