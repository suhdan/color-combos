<template>
  <section class="top-combos">
    <h2>Most Popular</h2>
    <ul v-if="!loading">
      <li :key="combo.id" v-for="combo in topCombos">
        <button 
          v-bind:style="{background: combo.color_two, color: combo.color_one}" 
          v-on:click="changeColor(combo.color_one)"
        >
          {{combo.color_one}}        
          <div 
            class="connector left"
            v-bind:style="{background: combo.color_one}">
          </div>
        </button>
        <button
          v-bind:style="{background: combo.color_one, color: combo.color_two}" 
          v-on:click="changeColor(combo.color_two)"
        >
          {{combo.color_two}}        
          <div 
            class="connector right"
            v-bind:style="{background: combo.color_two}">
          </div>
        </button>
      </li>
    </ul>
    <div v-else>
      <div class="rainbow-placeholder"></div>
    </div>
  </section>
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

<style lang="scss">
.top-combos {
  h2 {
    margin: 5px 0;
    text-align: center;
  }

  ul {
    display: flex;
    margin: 0 auto;
    overflow: hidden;
    overflow-x: scroll;
    padding: 0 5px;

    li > button {
      width: calc(100vw / 2.5);
      padding: 15px 0;
      position: relative;
      overflow: hidden;
    }
  }

  .connector {
    position: absolute; 
    width: 15px;
    height: 15px;
    transform: rotate(45deg);
  }
  .connector.left {
    bottom: -10px;
    left: 40%;
  }
  .connector.right {
    top: -10px;
    left: 51%;
  }

  .rainbow-placeholder {
    width: 100%;
    height: 92px;
    opacity: 0.2;
    animation: rainbow 5s linear alternate infinite;
    background: #ff0000;
  }
}

@keyframes rainbow {
	0% {
		background-color: #ff0000;
	}
	17% {
		background-color: #ffc000;
	}
	34% {
		background-color: #1aff00;
	}
	51% {
		background-color: #00ffff;
	}
	68% {
		background-color: #3900ff;
	}
	85% {
		background-color: #9700ff;
	}
	100% {
		background-color: #ff0000;
	}
}

@media(min-width: 600px) {
  .top-combos {
    ul {
      flex-direction: column;
      align-items: center;
      width: 50%;
      li {
        width: 100%;
        display: flex;  
      }
      li > button {
        width: 50%;
      }
    }
  }
}
</style>
