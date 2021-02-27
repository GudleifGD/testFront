<template>
    <div class="product-list">
        <product-item
            v-for="product in products"
            :key="product.id"
            :name="product.name"
            :image="product.image"
            :price="product.price"
            :description="product.description"
        ></product-item>
    </div>
</template>

<script>
import ProductItem from './ProductItem.vue';
export default {
  components: {ProductItem  },
    name: "ProductList",
    data() {
        return {
            products: { }
        }
    },
    mounted: function() {
        fetch('/products.json')
            .then(result => result.json())
            .then(data => {
                this.products = data.products.sort(function( a, b ) {
                    return (a.price - b.price);
                })
            })
    },
    methods: {
        
    }
};
</script>

<style lang="sass" scoped>
.product-list
    padding: 32px 24px 
    width: 100%
    display: flex 
    justify-content: space-evenly
    flex-wrap: wrap
    background: #f4f7fe
</style>