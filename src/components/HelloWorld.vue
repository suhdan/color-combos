<template>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
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
