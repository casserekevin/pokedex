<template>
  <Application/>
</template>

<script>
import Application from './components/Application'

export default {
  name: 'App',
  components: {
    Application
  }
}
</script>

<style>
  *{
    box-sizing: border-box;
  }

  html, body{
    margin: 0px;
    padding: 0px;
  }

  html {
    min-height: 100vh;
  }
</style>
