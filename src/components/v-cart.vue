<template>
  <div class="v-cart">
    <router-link :to="{name: 'catalog'}">
      <div class="v-cart__link_to_catalog">Back to catalog</div>
    </router-link>
    <h1>CART</h1>
    <p v-if="!cart_data.length">There are no products in cart</p>
    <v-cart-item
        v-for="(item,index) in cart_data"
        :key="item.article"
        :cart_item_data="item"
        @deleteFromCart="deleteFromCartItem(index)"
        @increment="increment(index)"
        @decrement="decrement(index)"
    >

    </v-cart-item>
    <div class="v-cart__total">
      <p class="total_name">Total:</p>
      <p>{{ cartTotalCost }}</p>
    </div>
  </div>
</template>

<script>
import vCartItem from './v-cart-item'
import {mapActions} from 'vuex'

export default {
  name: "v-cart",
  components: {
    vCartItem

  },
  props: {
    cart_data: {
      type: Array,
      default() {
        return []
      }

    }
  },
  computed: {
    cartTotalCost() {
      let result = []
      if (this.cart_data.length) {
        for (let item of this.cart_data) {
          result.push(item.price * item.quantity)
        }
        result = result.reduce(function (sum, el) {
          return sum + el;
        })
        return result;
      } else {
        return 0
      }
    }
  },
  methods: {
    ...mapActions([
      'DELETE_FROM_CART',
      'DECREMENT_CART_ITEM',
      'INCREMENT_CART_ITEM'
    ]),
    deleteFromCartItem(index) {
      this.DELETE_FROM_CART(index)
    },
    decrement(index){
      this.DECREMENT_CART_ITEM(index)
    },
    increment(index){
      this.INCREMENT_CART_ITEM(index)
    }
  }
}
</script>

<style scoped>
.v-cart {
  margin-bottom: 100px;
}

.v-cart__link_to_catalog {
  position: absolute;
  top: 10px;
  right: 10px;
  padding: 16px;
  border: 1px solid gray;
}

.v-cart__total {
  position: fixed;
  bottom: 0;
  right: 0;
  left: 0;
  padding: 24px;
  display: flex;
  justify-content: center;
  color: #e0e0e0;
  font-size: 20px;
  background: #26ae68;

}

.total_name {
  margin-right: 16px;
}

</style>