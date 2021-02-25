<template>
  <div class="v-catalog-item">
    <img class="v-catalog-item__image" :src="require('../assets/images/' + product_data.image)" alt="">
    <p class="v-catalog-item__name">{{product_data.name}}</p>
    <p class="v-catalog-item__price">{{ product_data.price }}</p>
    <button class="v-catalog-item__add_to_cart" @click="addToCart">Add</button>
  </div>
</template>

<script>
export default {
  name: "v-catalog-item",
  props: {
    product_data:{
      type: Object
    }
  },
  methods:{
    addToCart(){
      this.$emit('addToCart',this.product_data)
    }

  },
  mounted() {
    this.$set(this.product_data,'quantity',1)
  }
}
</script>

<style scoped>
.v-catalog-item {
  flex-basis: 25%;
  box-shadow: 0 0 8px 0 #e0e0e0;
  padding: 16px;
  margin-bottom: 16px;
}
.v-catalog-item__image{
  width: 100px;
}
button{
  padding: 8px 16px;
  color: #e0e0e0;
  background-color: #26ae68;
  border: none;
}
</style>