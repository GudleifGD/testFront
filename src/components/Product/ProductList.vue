<template>
    <div class="product-list">
        <product-item 
            v-bind:key='productTest.id'
            v-bind:name='productTest.name'
            v-bind:price='productTest.price'
            v-bind:image='productTest.image'
            v-bind:description='productTest.description'
        ></product-item>
        <product-item 
            v-bind:key='productTest.id + 1'
            v-bind:name='productTest.name'
            v-bind:price='productTest.price'
            v-bind:image='productTest.image'
            v-bind:description='productTest.description'
        ></product-item>
        <product-item 
            v-bind:key='productTest.id + 2'
            v-bind:name='productTest.name'
            v-bind:price='productTest.price'
            v-bind:image='productTest.image'
            v-bind:description='productTest.description'
        ></product-item>
        <product-item 
            v-bind:key='productTest.id + 3'
            v-bind:name='productTest.name'
            v-bind:price='productTest.price'
            v-bind:image='productTest.image'
            v-bind:description='productTest.description'
        ></product-item>
        <product-item 
            v-bind:key='productTest.id + 4'
            v-bind:name='productTest.name'
            v-bind:price='productTest.price'
            v-bind:image='productTest.image'
            v-bind:description='productTest.description'
        ></product-item>
        <product-item 
            v-bind:key='productTest.id + 5'
            v-bind:name='productTest.name'
            v-bind:price='productTest.price'
            v-bind:image='productTest.image'
            v-bind:description='productTest.description'
        ></product-item>
    </div>
</template>

<script>
import ProductItem from './ProductItem.vue';
export default {
  components: { ProductItem },
    name: "ProductList",
    data() {
        return {
            productTest: {
                id: 1,
                name: 'Apple iPhone 12',
                price: 29999,
                image: "2.jpg",
                description: "The iPhone 12 display has rounded corners that follow a beautiful curved design, and these corners are within a standard rectangle. "
            }
        }
    }
};
</script>

<style lang="sass" scoped>
.product-list
    padding: 32px 24px 
    width: 100%
    display: flex 
    justify-content: space-around
    flex-wrap: wrap
    background: #f4f7fe
</style>