<template>
  <div class="color-input">
    <h2>Choose a color</h2>
    <Chrome :value="color" @input="handleInput"/>
  </div>
</template>

<script>
import { Chrome } from 'vue-color'

export default {
  name: 'ColorInput',
  components: {
    Chrome
  },
  props: {
    changeColor: Function,
    color: String
  },
  created: function() {
    this.handleInput({ hex: '#000000' })
  },
  methods: {
    handleInput: function(e) {
      this.changeColor(e.hex)
    }
  }
}
</script>

<style lang="scss">
.color-input {
  h2 {
    margin-bottom: 10px;
    text-align: center;
  }
  .vc-chrome {
    width: 100%;
  }
}
</style>
