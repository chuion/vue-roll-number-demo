<template>
  <div style="width: 320px; margin: 0 auto" id="app">
    <PageOne />
    <PageTwo />
    <roll-counter />
  </div>
</template>

<script>
import RollCounter from './components/RollCounter';
import PageOne from './views/PageOne'
import PageTwo from './views/PageTwo'

export default {
  name: "App",
  components: {
    PageOne,
    PageTwo,
    RollCounter
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
