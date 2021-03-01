<template>
  <div class="currency-control">
    <span>Валюта</span>
    <div>
      <input type="radio" id="UAH" value="UAH" v-model="currency" />
      <label for="UAH" v-bind:class="[defualtCurrency() ? 'shadow' : '']">
        UAH
      </label>
      <input type="radio" id="USD" value="USD" v-model="currency" />
      <label for="USD" v-bind:class="[!defualtCurrency() ? 'shadow' : '']"
        >USD</label
      >
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currency: "UAH"
    };
  },
  watch: {
    currency: function() {
      this.$store.commit("currencyValue", this.currency);
    }
  },
  methods: {
    defualtCurrency: function() {
      if (this.currency == "UAH") {
        return true;
      } else {
        return false;
      }
    }
  }
};
</script>

<style lang="sass" scoped>
.currency-control
    display: flex
    flex-direction: column
    margin-bottom: 24px
    &>span
        font-style: normal
        font-weight: 800
        font-size: 24px
        line-height: 120%
        letter-spacing: 0.03em
        margin-bottom: 16px
    &>div
        display: flex
        justify-content: center
        input
            display: none
        label
            border: 2px solid #000000
            padding: 6px 10px
            font-style: normal
            font-weight: bold
            font-size: 18px
            line-height: 120%
            background: #E5E5E5
            opacity: 0.5
            transition: 0.3s
            cursor: pointer
            &:hover
                opacity: 1
            &:first-of-type
                border-right: none
                border-radius: 16px 0 0 16px
            &:last-of-type
                border-radius: 0 16px 16px 0
            &.shadow
                background: #fff
                opacity: 1
</style>
