<template>
  <div>
    <h2 class="mb-3">Tellimused</h2>
        <b-table striped hover :items="items"></b-table>
    <!-- <p>Count: {{count}}</p>
    <button @click="addCount()">+</button>
    <button @click="removeCount()">-</button> -->
  </div>
</template>
<script>
import axios from 'axios'


export default {
  name: 'Orders',
  data() {
    return {
      
      count: 0,
      
        fields: ['orderID', 'toWhom', 'toCity'],
        items: [],
    }
  },
  async created () {
    const orders = await axios({
      url: 'api/orders',
      method: 'GET',
      headers: {}
    })
    console.log('orders', orders)

    this.items = orders.data.allOrders
  },
  methods: {
    addCount () {
      console.log('Praegune count:', this.count)
      this.count++
    },
    removeCount () {
      console.log('Praegune count:', this.count)
      this.count--

      
    }
  }
}
</script>
