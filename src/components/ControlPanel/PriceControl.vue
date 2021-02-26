<template>
    <div class="price-panel">
        <span>Цена</span>
        <div>
            <div>
                <span>от:</span>
                <input type="number" name="PriceFrom" id="PriceFrom" v-model="priceFilter.from">
            </div>
            <div>
                <span>до:</span>
                <input type="number" name="PriceTo" id="PriceTo" v-model="priceFilter.to">
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "PriceControl",
    data() {
        return {
            priceFilter: {
                from: 0,
                to: 10000
            }
        }
    }
}
</script>

<style lang="sass" scoped>
.price-panel
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
        justify-content: space-between
        &>div 
            display: flex 
            flex-direction: column
            span
                font-style: normal
                font-weight: 600
                font-size: 16px
                line-height: 19px
                color: #222222
            input
                font-style: normal
                font-weight: 600
                font-size: 16px
                line-height: 19px
                color: #222222
                max-width: 150px
</style>