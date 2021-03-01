<template>
  <div class="product-list">
    <transition-group>
      <product-item
        v-for="product in productsState"
        :key="product.id"
        :name="product.name"
        :image="product.image"
        :price="product.price"
        :description="product.description"
      ></product-item>
    </transition-group>
  </div>
</template>

<script>
import ProductItem from "./ProductItem.vue";

export default {
  components: { ProductItem },
  name: "ProductList",
  data() {
    return {
      products: [],
    };
  },
  created() {
    fetch("/products.json")
      .then((result) => result.json())
      .then((data) => {
        this.products = data.products.sort(function (a, b) {
          return a.price - b.price;
        });
        this.setRangePrice();
        this.products.forEach((item) => (item.priceUah = item.price));
        this.products.forEach(
          (item) => (item.priceUsd = Math.round(item.price / 28))
        );
      });
  },
  watch: {
    sortType: function () {
      const mapper = {
        priceDown: () => {
          this.products = oldProducts.sort(function (a, b) {
            return b.price - a.price;
          });
        },
        priceUp: () => {
          this.products = oldProducts.sort(function (a, b) {
            return a.price - b.price;
          });
        },
        abc: () => {
          this.products = oldProducts.sort(function (a, b) {
            var nameA = a.name.toLowerCase(),
              nameB = b.name.toLowerCase();
            if (nameA < nameB) return -1;
            if (nameA > nameB) return 1;
            return 0;
          });
        },
      };

      let oldProducts = this.products;

      return mapper[this.sortType]();
    },
    currencyValue: function () {
       const mapper = {
        UAH: () => {
          this.products.forEach((item) => (item.price = item.priceUah));
        },
        USD: () => {
          this.products.forEach((item) => (item.price = item.priceUsd))
        }
      };
      mapper[this.currencyValue]();
      this.setRangePrice();
    },
  },
  computed: {
    productsState() {
      return this.products.filter(
        (product) =>
          this.minValueSort <= product.price &&
          this.maxValueSort >= product.price
      );
    },
    sortType() {
      return this.$store.state.sortType;
    },
    maxValueSort() {
      return this.$store.state.maxPrice;
    },
    minValueSort() {
      return this.$store.state.minPrice;
    },
    currencyValue() {
      return this.$store.state.currency;
    },
  },
  methods: {
    setRangePrice() {
      let maxValue = Math.max.apply(
        null,
        this.products.map((item) => item.price)
      );
      this.$store.commit("maxPriceValue", maxValue);
      let minValue = Math.min.apply(
        null,
        this.products.map((item) => item.price)
      );
      this.$store.commit("minPriceValue", minValue);
    },
  },
};
</script>

<style lang="sass" scoped>
.product-list
  width: 100%
  &>span
    padding: 32px 24px
    width: 100%
    height: 100%
    display: flex
    justify-content: space-evenly
    flex-wrap: wrap
    background: #f4f7fe
</style>
