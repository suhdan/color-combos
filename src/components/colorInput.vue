<template>
  <div class="color-input">
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

<style lang="scss">
.color-input {
  .vc-chrome {
    width: 100%;
  }
}
</style>
