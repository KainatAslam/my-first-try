<template>
  <div id="app">
    <AppHeader/>
    <b-container>
      <b-row class="justify-content-center">
        <AddProduct @addProduct="addProduct"/>
        <ListProduct :products="productList" @updateProduct="updateProduct" @deleteProduct="deleteProduct"/>
      </b-row>
    </b-container>
  

  </div>
</template>

<script>

import AppHeader from './components/AppHeader.vue'
import AddProduct from './components/AddProduct.vue'
import ListProduct from './components/ListProduct.vue'
// import UpdateProduct from './components/UpdateProduct.vue'
import axios from 'axios'
export default {
  name: 'App',
  components:{
    AppHeader  ,
  AddProduct,
ListProduct ,
 },
data(){
  return {
    productList: []
  }
},
methods: {
 async getProductList() {
  try{
    let result = await axios.get('/db.json');
    console.log('Data', result.data)
    this.productList = result.data;
  } catch(error) {
    console.log('error', error)
  }
  },
 async  addProduct(newProduct){
    console.log('newProduct',newProduct);
    try{
      await axios.post('/db.json', newProduct)
      this.getProductList();
    } catch(error){
      console.log('Error',error)
    }
  },
  async deleteProduct(productId){
    console.log('newProduct',productId);
    try{
      await axios.delete(`/db.json/${productId}`)
      this.getProductList();
    }
    catch(error){
        console.log("Error",error)
    }
  },
  async updateProduct(updateProduct){
    console.log('*****',updateProduct);
    try{
      await axios.put(`/db.json/${updateProduct.id}`,updateProduct )
      this.getProductList();
    }
    catch(error){
        console.log("Error",error)
    }
  },
  
},
mounted(){
  this.getProductList();
},

}
</script>

<style>
.error-message{
  color:red
}
</style>
