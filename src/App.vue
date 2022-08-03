<template>
  <Navbar :cart-total="cartTotal" :cart-qty="cartQty" />
  <div class="container">
    <router-view :products="products" :cart-total="cartTotal" />
  </div>
</template>

<script>
import { provide, reactive } from 'vue'
import Navbar from '@/components/Navbar'

export default {
  components: {
    Navbar
  },
  data: function() {
    return {
      products: []
    }
  },
  created() {
    fetch('https://hplussport.com/api/products/order/price')
      .then(response => response.json())
      .then(data => {
        this.products = data
      })
  },
  setup() {
    const cart = reactive([])

    function addItem(product) {
      let whichProduct
      let existing = cart.filter(function(item, index) {
        if (item.product.id == Number(product.id)) {
          whichProduct = index
          return true
        } else {
          return false
        }
      })

      if (existing.length) {
        cart[whichProduct].qty++
      } else {
        cart.push({ product: product, qty: 1 })
      }
    }

    function deleteItem(id) {
      if (cart[id].qty > 1) {
        cart[id].qty--
      } else {
        cart.splice(id, 1)
      }
    }

    provide('appCart', cart)
    provide('addItem', addItem)
    provide('deleteItem', deleteItem)

    return {
      cart,
      addItem,
      deleteItem
    }
  },
  computed: {
    cartTotal() {
      let sum = 0
      for (let key in this.cart) {
        sum = sum + this.cart[key].product.price * this.cart[key].qty
      }
      Number(sum)
      return sum
    },
    cartQty() {
      let qty = 0
      for (let key in this.cart) {
        qty = qty + this.cart[key].qty
      }
      return qty
    }
  }
}
</script>

<style lang="scss">
$primary: #6f42c1;
@import 'node_modules/bootstrap/scss/bootstrap';
</style>
