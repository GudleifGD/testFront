<template>
    <div class="sort-panel">
        <span>Сортировка</span>
        <div>
            <input type="radio" id="priceUp" value="priceUp" v-model="sortType">
        <label for="priceUp">По возрастанию цены</label>
        </div>
        <div>
            <input type="radio" id="priceDown" value="priceDown" v-model="sortType">
        <label for="priceDown">По убыванию цены</label>
        </div>
        <div>
            <input type="radio" id="abc" value="abc" v-model="sortType">
            <label for="abc">по алфавиту</label>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            sortType: "priceUp"
        }
    }
}
</script>

<style lang="sass" scoped>
.sort-panel
    display: flex 
    flex-direction: column
    &>span 
        font-style: normal
        font-weight: 800
        font-size: 24px
        line-height: 120%
        letter-spacing: 0.03em
        margin-bottom: 16px
    &>div 
        margin-bottom: 8px
        label
            margin-left: 4px
            position: relative
            &:hover
                &::after
                    width: 24px
            &::after
                content: ''
                position: absolute
                top: 9px
                transition: 0.3s
                right: -36px
                width: 0
                height: 2px
                background: rgba(0, 0, 0, 0.4)

</style>