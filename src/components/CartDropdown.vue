<template>
  <div class="dropdown-clip">
    <transition name="dropdown">
      <div
        v-if="displayCart"
        class="list-group bg-white"
        aria-labelledby="cartDropdown"
      >
        <div v-for="(item, index) in navCart" :key="index">
          <div class="dropdown-item-text text-nowrap text-right align-middle">
            <span class="badge bg-success align-text-top mr-1">{{
              item.qty
            }}</span>
            {{ item.product.name }}
            <b>
              <curr :amt="item.qty * Number(item.product.price)" />
            </b>
            <button
              @click.stop="deleteItem(index)"
              class="btn btn-sm btn-danger ml-2"
              aria-label="delete item"
            >
              <span aria-hidden="true">-</span>
            </button>
          </div>
        </div>
        <router-link
          to="/checkout"
          class="btn btn-sm btn-success text-white float-right mr-2 mt-2"
          >checkout</router-link
        >
      </div>
    </transition>
  </div>
</template>

<script>
import { inject } from 'vue'
import Curr from '@/components/Curr.vue'

export default {
  components: { Curr },
  props: ['displayCart'],
  setup() {
    const navCart = inject('appCart', [])
    const deleteItem = inject('deleteItem')

    return { navCart, deleteItem }
  }
}
</script>

<style>
.dropdown-clip {
  overflow: hidden;
}

.dropdown-enter-active,
.dropdown-leave-active {
  transition: all 0.5s ease-in-out;
  transform: auto;
}

.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: translateY(-300px);
}
</style>
