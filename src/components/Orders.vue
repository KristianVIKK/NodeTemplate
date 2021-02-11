<template>
  <div>
    <h2 class="mb-3">Tellimused</h2>
       <!-- Tellimuse tabel -->
    <b-table striped hover :items="items" :fields="fields">

    

      <template #cell(actions)="data">
        <b-button v-b-modal.modal-1 variant="success" @click="showProducts(data.item.products, data.item)">Vaata tooteid</b-button>
      </template>

    </b-table>

    <!-- Toote tabel -->
    <!-- TODO: Add real data -->
    
    <!-- <p>Count: {{count}}</p>
    <button @click="addCount()">+</button>
    <button @click="removeCount()">-</button> -->

  <b-modal id="modal-1" :title="productTableTitle" size='xl'>
    <b-table striped hover :items="productItems" :fields="productFields">
      <template #cell(price)="data">
        <b class="text-info">{{ data.value }} EUR</b>
      </template>
    </b-table>
  </b-modal>


  </div>
</template>
<script>
import axios from 'axios'


export default {
  name: 'Orders',
  data() {
    return {
      
      count: 0,
      
      fields: [ {key:'orderID', label: 'Tellimuse ID'}, {key:'toWhom', label: 'Kellele'}, {key:'orderingDate', label: 'Tellimuse kp.'}, {key:'toCounty', label: 'Riik'}, {key:'toCity', label: 'Linn'},{key:'toStreet', label: 'Tänav'}, {key:'toHouse', label: 'Maja/korteri nr.'}, {key:'status', label: 'Staatus'},  'actions'],
      items: [],
      productFields: [],
      productItems: [],
      productTableTitle: 'Pealkiri'
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
    showProducts (products, item) {
      console.log('products', products)
      this.productItems = products
      console.log(item)
      this.productTableTitle = item.orderNumber
    },
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
