<template>
  <div class="control-panel">
    <price-control></price-control>
    <currency-control></currency-control>
    <sort-control></sort-control>
  </div>
</template>

<script>
import CurrencyControl from "./CurrencyControl.vue";
import PriceControl from "./PriceControl.vue";
import SortControl from "./SortControl.vue";
export default {
  components: {
    PriceControl,
    CurrencyControl,
    SortControl,
  },
};
</script>

<style lang="sass" scoped>
.control-panel
    display: flex
    flex-direction: column
    max-width: 350px
    padding: 24px
    border-right: 2px solid rgba(0, 0, 0, 0.2)
    height: 100%
</style>
