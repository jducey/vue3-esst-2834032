<template>
  <div class="container">
    <h1>Checkout</h1>

    <table class="table table-hover" v-if="checkoutCart.length">
      <caption class="text-right h3">
        <b>Total:</b>
        <curr :amt="cartTotal" />
      </caption>
      <thead>
        <tr>
          <th scope="col"></th>
          <th scope="col">Item</th>
          <th scope="col" class="text-center">Qty</th>
          <th scope="col" class="text-right">Price</th>
          <th scope="col" class="text-right">Sub-total</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in checkoutCart" :key="item.product.id">
          <td class="text-center">
            <div class="btn-group" role="group" aria-label="Basic example">
              <button
                @click="addItem(item.product)"
                class="btn btn-success"
                aria-label="add item"
              >
                <span aria-hidden="true">+</span>
              </button>
              <button
                @click="deleteItem(index)"
                class="btn btn-outline-success"
                aria-label="delete item"
              >
                <span aria-hidden="true">-</span>
              </button>
            </div>
          </td>
          <th scope="row">{{ item.product.name }}</th>
          <td class="text-center">{{ item.qty }}</td>
          <td class="text-right">
            <curr :amt="Number(item.product.price)" />
          </td>
          <td class="text-right">
            <curr :amt="item.qty * Number(item.product.price)" />
          </td>
        </tr>
      </tbody>
    </table>
    <router-link class="btn btn-sm btn-success" to="/">
      Keep Shopping
    </router-link>
  </div>
</template>

<script>
import { inject } from 'vue'
import Curr from '@/components/Curr'

export default {
  components: { Curr },
  props: ['cartTotal'],
  setup() {
    const checkoutCart = inject('appCart', [])
    const addItem = inject('addItem')
    const deleteItem = inject('deleteItem')

    return { checkoutCart, addItem, deleteItem }
  }
}
</script>

<style></style>
