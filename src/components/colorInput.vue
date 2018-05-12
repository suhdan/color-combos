<template>
  <div className="color-input">
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
  methods: {
    handleInput: function(e) {
      this.changeColor(e.hex)
    }
  }
}
</script>

<style>
</style>
