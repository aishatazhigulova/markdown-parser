<template>
  <div id="app">
    <Markdown />
  </div>
</template>

<script>
import Markdown from "@/components/Markdown";

export default {
  name: 'App',
  components: {
      Markdown,
  }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #FFFFFF;
    background-color: #2c3e50;
    width: 100vw;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    overflow: hidden;
}

@media only screen and (max-width: 600px) {
    #app {
        padding: 20px;
    }
}
</style>
