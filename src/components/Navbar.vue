<template>
  <nav class="navbar navbar-light sticky-top mr-3">
    <div
      v-if="navCart.length"
      class="w-100 navbar-text d-flex justify-content-end position-absolute top-0"
    >
      <div
        class="bg-white d-flex align-items-end flex-column bd-highlight mb-3"
      >
        <div class="mb-2">
          <span class="font-weight-bold bg-white"
            ><curr :amt="cartTotal"
          /></span>
          <button
            @click="toggleCartMenu"
            class="btn btn-sm btn-success ml-3"
            id="cartDropdown"
            aria-haspopup="true"
            aria-expanded="false"
          >
            <fa icon="fa-shopping-cart mr-1" />
            {{ cartQty }}
          </button>
        </div>
        <cart-dropdown :display-cart="displayCart" />
      </div>
    </div>
  </nav>
</template>

<script>
import { inject } from 'vue'
import Curr from '@/components/Curr'
import CartDropdown from '@/components/CartDropdown'

export default {
  data: function() {
    return {
      displayCart: false
    }
  },
  setup() {
    const navCart = inject('appCart', [])

    return { navCart }
  },
  components: { Curr, CartDropdown },
  props: ['cartTotal', 'cartQty'],
  methods: {
    toggleCartMenu() {
      this.displayCart = !this.displayCart
    }
  }
}
</script>
