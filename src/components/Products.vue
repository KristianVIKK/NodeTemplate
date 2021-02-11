<template>
  <div>
    <h2 class="mb-3">Tooted</h2>
       <!-- Toodete tabel -->
    <b-table striped hover :items="items" :fields="fields">

    

      <!-- <template #cell(actions)="data">
        <b-button v-b-modal.modal-1 variant="success" @click="showProducts(data.item.products, data.item)">Vaata tooteid</b-button>
      </template> -->

    </b-table>

    <!-- Toote tabel -->
    <!-- TODO: Add real data -->
    
    <!-- <p>Count: {{count}}</p>
    <button @click="addCount()">+</button>
    <button @click="removeCount()">-</button> -->

 
    <!-- <b-table striped hover :items="items">
      <template #cell(productPrice)="data">
        <b class="text-info">{{ data.productPrice }} EUR</b>
      </template> -->
    </b-table>
  


  </div>
</template>
<script>

import axios from 'axios'



export default {
  name: 'Products',
  data() {
    return {
      
      count: 0,
      
      

      fields: [{key:'_id', label: 'Toote ID'}, {key: 'productName', label: 'Tootenimi'}, {key: 'productCat', label: 'Kategooria'}, 
      {key: 'productQty', label: 'Kogus'}, {key: 'productDescription', label: 'Tootekirjeldus'}, { key: 'productPrice.$numberDecimal', label: 'Hind' }],
      items: [],
      
     
    }
  },
  async created () {
    const products = await axios({
      url: 'api/products',
      method: 'GET',
      headers: {}
    })
    

    this.items = products.data.allProducts

  },
  methods: {
    showProducts (products) {
      
      this.productItems = products
      
    }

      
    }
  }

</script>