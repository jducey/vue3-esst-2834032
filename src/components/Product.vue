<template>
  <div class="col-2 m-auto">
    <button
      @click="addItem(item)"
      class="btn btn-success"
      aria-label="add item to cart"
    >
      <span aria-hidden="true">+</span>
    </button>
  </div>
  <div class="col-sm-4">
    <img class="img-fluid d-block" :src="item.image" :alt="item.name" />
  </div>
  <div class="col">
    <h3 class="text-primary">{{ item.name }}</h3>
    <p class="mb-0">{{ item.description }}</p>
    <div class="h5 float-end">
      <span class="label"></span><curr :amt="item.price" />
    </div>
  </div>
</template>

<script>
import { inject } from 'vue'
import Curr from '@/components/Curr'
export default {
  props: ['item'],
  setup() {
    const addItem = inject('addItem')

    return { addItem }
  },
  components: { Curr }
}
</script>
