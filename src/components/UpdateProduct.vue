<template>
    <div>
        <b-button  @click="modalShow = !modalShow"><i  class="fa-thin fa-pen-to-square">Edit</i></b-button>
      <b-modal 
      v-model="modalShow"
      title="Update Product"
      @show="showModal"
      @hidden="resetModal"
      @ok="handleSubmit"
    >
      
      <b-form autocomplete="off">
           
           <b-form-group
               label="Enter your name">
               <b-form-input v-validate="{required:true, min:3}" v-model="form.name" id="name" name="name" trim></b-form-input>
               <div v-if="submitted" class="error-message">
                   {{ errors.first('name') }}
               </div>
           </b-form-group>
       
       <b-form-group
           label="Price ($)">
           <b-form-input v-validate="{required:true, numeric:true}" v-model="form.price" id="Price" name="price" trim></b-form-input>
           <div v-if="submitted" class="error-message">
                   {{ errors.first('price') }}
               </div>
       </b-form-group>
       <b-form-group
           label="brand">
           <b-form-input v-validate="{required:true}" v-model="form.brand" id="brand" name="brand" trim></b-form-input>
           <div v-if="submitted" class="error-message">
                   {{ errors.first('brand') }}
               </div>
       </b-form-group>
       <b-form-group
           label="Inventory">
           <b-form-radio v-validate="{required:true}" v-model='form.InventoryStatus' name="InventoryStatus" value="true">In Stock</b-form-radio>
           <b-form-radio v-validate="{required:true}" v-model='form.InventoryStatus' name="InventoryStatus" value="false">Out Of Stock</b-form-radio>
           <div v-if="submitted" class="error-message">
                   {{ errors.first('InventoryStatus') }}
               </div>
       </b-form-group>
   </b-form>
    </b-modal>
    </div>
     
</template>

<script>
 export default {
    name:"UpdateProduct",
    props:['product'],
    data(){
        return{
            modalShow: false ,   
            form:{
            name:'',
            price:'',
            brand:'',
            InventoryStatus:'',
        },
        submitted:false
        }
        
    },
    methods:{
        showModal(){
            console.log('model opened');
            this.form={
                name: this.$props.product.name,
                price: this.$props.product.price.split('$')[1],
                brand: this.$props.product.brand,
                InventoryStatus: this.$props.product.InventoryStatus.toString(),
            }
        },
        resetModal(){
            console.log('model closed');
            this.form = {};
},
        async handleSubmit(bvModalEvt){
            bvModalEvt.preventDefault()
            console.log('submitted');

             this.submitted= true
        let result = await this.$validator.validate()
        console.log('Result', result)
        if(result){
           this.$emit('updateProduct', {
            name:this.form.name,
            price:'$' + this.form.price,
            brand: this.form.brand,
            InventoryStatus: this.form.InventoryStatus ==='true',
            id: this.$props.product.id
           })
           
            this.modalShow = false;
            this.submitted = false;
        }

},
    }
 }
</script>
<style></style>