<template>
  <div v-on:click="changeColor('white')">
      hi
  </div>
</template>

<script>
export default {
  name: 'TopColorCombos',
  props: {
    changeColor: Function
  }
}
</script>

<style>
</style>
