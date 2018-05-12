<template>
  <div id="app">
    <header>
      <h1>Color Combos</h1>
    </header>
    <main>
      <TopColorCombos :changeColor="changeColor"/>
      <ColorInput v-bind:color="color" :changeColor="changeColor"/>
      <ColorComboResults v-bind:color="color"/>
    </main>
  </div>
</template>

<script>
import TopColorCombos from './components/topColorCombos.vue'
import ColorInput from './components/colorInput.vue'
import ColorComboResults from './components/colorComboResults.vue'

export default {
  name: 'app',
  components: {
    TopColorCombos,
    ColorInput,
    ColorComboResults
  },
  data() {
    return {
      color: 'transparent'
    }
  },
  methods: {
    changeColor: function(color) {
      this.color = color
    }
  }
}
</script>

<style>
  body {
    height: 100vh;
    width: 100%;
    font-size: 16px;
    font-family: 'Lobster', cursive;
    background-color: #404040;
    color: #ffffff;
  }

  header {
    width: 100%;
    text-align: center;
    font-size: 7em;
  }

  main {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  main > div {
    margin: 10px;
  }

  @media(min-width: 600px) {
    body {
      font-size: 12px;
    }
    main {
      flex-direction: row;
    }
  }
</style>
