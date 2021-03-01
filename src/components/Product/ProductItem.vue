<template>
  <div class="product-item">
    <img v-bind:src="productImage" v-bind:alt="name" />
    <div>
      <h5>
        {{ name }}
      </h5>
      <span>
        {{ price }}
      </span>
      <p>
        {{ description }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductItem",
  props: {
    name: String,
    price: Number,
    image: String,
    description: String,
    baseImage: Boolean
  },
  computed: {
    productImage() {
      if (this.baseImage == false) {
      return require(`@/assets/products/${this.image}`);
      } else {
        return this.image
      }
    }
  }
};
</script>

<style lang="sass" scoped>
.product-item
    display: flex
    align-items: center
    padding: 24px
    box-shadow: 0 10px 40px rgb(5 6 24 / 5%)
    max-width: 450px
    width: 100%
    height: 300px
    border-radius: 8px
    background: #ffffff
    transition: all ease-in 0.5s
    margin-bottom: 34px
    &:hover
        transform: translateY(-12px)
    img
        max-width: 120px
        width: auto
        max-height: 120px
    &>div
        display: flex
        flex-direction: column
        margin-left: 24px
        h5
            margin: 0 0 16px
            font-style: normal
            font-weight: 500
            font-size: 16px
            line-height: 19px
            color: #222222
        span
            margin: 0 0 16px
            font-style: normal
            font-weight: 700
            font-size: 14px
            line-height: 17px
            color: #222222
        p
            margin: 0
            font-style: normal
            font-weight: 500
            font-size: 14px
            line-height: 17px
            color: #222222
</style>
