<template>
  <div class="add-panel">
    <form>
      <div class="add-panel-text">
        <div>
          <div>
            <label for="title">Имя</label>
            <input
              type="text"
              name="title"
              id="title"
              :class="{ err: errText }"
              @change="validName()"
              min="1"
              v-model="title"
            />
          </div>
          <div>
            <label for="price"> Цена </label>
            <input
              type="number"
              name="price"
              id="price"
              :class="{ err: errPrice }"
              @change="validPrice()"
              min="1"
              max="99999"
              v-model="price"
            />
          </div>
        </div>
        <textarea
          name="description"
          id="description"
          cols="30"
          rows="3"
          v-model="description"
          placeholder="Description"
        ></textarea>
      </div>
      <div class="add-panel-file">
        <label for="file">Изображение</label>
        <input
          type="file"
          name="file"
          id="file"
          @change="loadImage()"
          ref="file"
          accept="image/*"
        />
      </div>
      <div class="add-panel-button">
        <span @click="uploadItem()">{{ SaveBtn }}</span>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "AddPanel",
  data() {
    return {
      title: "",
      price: "",
      file: "",
      description: "",
      imageData: "",
      errText: false,
      errPrice: false,
      SaveBtn: 'Save'
    };
  },
  methods: {
    validName() {
      let regName = /^[a-z0-9]{3,25}$/;
      if (!regName.test(this.title)) {
        this.errText = true;
      } else {
        this.errText = false;
      }
    },
    validPrice() {
      let regName = /^[0-9]{3,5}$/;
      if (!regName.test(this.price)) {
        this.errPrice = true;
      } else {
        this.errPrice = false;
      }
    },
    loadImage() {
      this.file = this.$refs.file.files[0];
      let reader = new FileReader();
      reader.addEventListener(
        "load",
        function () {
          this.imageData = reader.result;
        }.bind(this),
        false
      );
      if (this.file) {
        if (/\.(jpe?g|png|gif)$/i.test(this.file.name)) {
          reader.readAsDataURL(this.file);
        }
      }
    },
    uploadItem() {
      let item = {};
      this.validName();
      this.validPrice();
      item.id = Math.floor(Math.random() * 1000);
      item.name = this.title;
      item.priceUah = item.price = Number(this.price);
      item.priceUsd = Math.floor(this.price / 28);
      item.description = this.description;
      item.baseImage = true;
      item.image = this.imageData;
      if (this.errText == true || this.errPrice == true)  { 
          this.SaveBtn = 'Error'
      } else {
        this.$store.commit("userProductAdd", item);
        this.SaveBtn = 'Ok!'
      }
    },
  },
};
</script>

<style lang="sass" scoped>
.add-panel
    width: 100%
    border-top: 2px solid rgba(0, 0, 0, 0.2)
    background: #F3F6EC
    height: 100%
    display: flex
    justify-content: center
    align-items: center
    form
        min-width: 500px
    &-text
        display: flex
        justify-content: space-between
        margin-bottom: 16px
        textarea
            width: 48%
            padding: 4px
            font-style: normal
            font-weight: 600
            font-size: 16px
            line-height: 19px
            color: #222222
            font-family: Avenir, Helvetica, Arial, sans-serif
        &>div
            width: 50%
            &>div
                display: flex
                justify-content: space-between
                align-items: center
                &:first-of-type
                    margin-bottom: 16px
                label
                    font-style: normal
                    font-weight: bold
                    font-size: 18px
                    line-height: 120%
                input
                    width: 100%
                    max-width: 200px
                    padding: 4px
                    font-style: normal
                    font-weight: 600
                    font-size: 16px
                    line-height: 19px
                    color: #222222
                    &.err
                        border: 2px solid red
    &-file
        display: flex
        align-items: center
        label
            font-style: normal
            font-weight: bold
            font-size: 18px
            line-height: 120%
            margin-right: 12px
    &-button
        display: flex
        justify-content: flex-end
        span
            border: 2px solid #000000
            padding: 8px 16px
            font-style: normal
            font-weight: bold
            font-size: 18px
            line-height: 120%
            background: #E5E5E5
            opacity: 0.8
            transition: 0.3s
            cursor: pointer
            border-radius: 16px
            &:hover
                opacity: 1
</style>