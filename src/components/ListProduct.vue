<template>
       <b-col md="4" class="m-3">
        <b-card
    header="List Product"
  >
  
      <b-card-group deck >
      <b-card 
    style="min-width: 50%"
        :border-variant="product.InventoryStatus ? 'success': 'danger' "
        align="center"
        class="m-3"
        v-for="product in products" :key="product.id"
      >
    
      <b-badge  class="danger" :variant="product.InventoryStatus ? 'success': 'danger'"> {{   product.InventoryStatus?'Available':'Not Available'}}</b-badge>
        <b-card-text> <strong>Name: </strong> {{ product.name }}</b-card-text>
        <b-card-text> <strong>Brand: </strong>{{ product.brand }}</b-card-text>
        <b-card-text> <strong>Price: </strong>{{ product.price }}</b-card-text>
            <hr/>
            <b-row>
              <b-col>
                 <b-button variant="danger" @click="deleteProduct(product.id)">
                <i class="fa-regular fa-trash">Delete</i>
              </b-button> </b-col>

              <b-col> 
              <UpdateProduct :product="product" @updateProduct ="updateProduct"/>
             </b-col>
            </b-row>
      </b-card>
    </b-card-group >
      

  </b-card>
    </b-col>
</template>

<script>
import UpdateProduct from './UpdateProduct.vue'
export default{
props: ['products'],
components:{
  UpdateProduct
},
methods:{
  deleteProduct(productId){
    this.$emit('deleteProduct',productId);
  },
  updateProduct(updateProduct){
this.$emit('updateProduct',updateProduct);
  }
} ,
}
</script>

<style>
</style>