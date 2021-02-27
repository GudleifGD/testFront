<template>
  <div class="product-list">
    <transition-group>
      <product-item
        v-for="product in products"
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
      products: []
    };
  },
  created() {
    fetch("/products.json")
      .then(result => result.json())
      .then(data => {
        this.products = data.products.sort(function(a, b) {
          return a.price - b.price;
        });
      });
  },
  updated() {
    let maxValue = Math.max.apply(
      null,
      this.products.map(item => item.price)
    );
    this.$store.commit("maxPriceValue", maxValue);
    let minValue = Math.min.apply(
      null,
      this.products.map(item => item.price)
    );
    this.$store.commit("minPriceValue", minValue);
  },
  watch: {
    sortType: function() {
      let oldProducts = this.products;
      if (this.sortType == "priceDown") {
        this.products = oldProducts.sort(function(a, b) {
          return b.price - a.price;
        });
      } else if (this.sortType == "priceUp") {
        this.products = oldProducts.sort(function(a, b) {
          return a.price - b.price;
        });
      } else if (this.sortType == "abc") {
        this.products = oldProducts.sort(function(a, b) {
          var nameA = a.name.toLowerCase(),
            nameB = b.name.toLowerCase();
          if (nameA < nameB) return -1;
          if (nameA > nameB) return 1;
          return 0;
        });
      }
    }
  },
  computed: {
    sortType() {
      return this.$store.state.sortType;
    },
    maxValueSort() {
      return this.$store.state.maxPrice;
    },
    minValueSort() {
      return this.$store.state.minPrice;
    }
  },
  methods: {}
};
</script>

<style lang="sass" scoped>
.product-list
    &>span
        padding: 32px 24px
        width: 100%
        height: 100%
        display: flex
        justify-content: space-evenly
        flex-wrap: wrap
        background: #f4f7fe
</style>
