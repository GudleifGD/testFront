<template>
  <div id="app">
    <div>
      <control-panel></control-panel>
      <product-list></product-list>
    </div>
    <add-panel></add-panel>
  </div>
</template>

<script>
import AddPanel from './components/AddPanel/AddPanel.vue';
import ControlPanel from "./components/ControlPanel/ControlPanel.vue";
import ProductList from "./components/Product/ProductList.vue";

export default {
  name: "App",
  components: {
    ControlPanel,
    ProductList,
    AddPanel
  }
};
</script>

<style lang="sass">
body
  margin: 0
  padding: 0

*
  box-sizing: border-box
#app
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  color: #2c3e50
  min-height: 100vh
  max-height: 100vh
  height: 100vh
  display: flex
  flex-direction: column
  &>div 
    display: flex
    max-height: 70%
</style>
