<template>
    <b-col md="4" class="m-3">
        <b-card
    header="Add Product">
    <b-card-body>

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
    </b-card-body>
   
    <b-button block variant="primary" @click="addProduct">Add Product</b-button>
  </b-card>
    </b-col>
    
</template>

<script>

export default{
   
data(){
    
    return{
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
    async addProduct(){
        this.submitted= true
        let result = await this.$validator.validate()
        if(result){
            this.$emit('addProduct', {
                name: this.form.name,
                price: '$'+ this.form.price,
                brand:this.form.brand,
                InventoryStatus: this.form.InventoryStatus === 'true',
            });
            this.form={
                name:'',
            price:'',
            brand:'',
            InventoryStatus:'',
            }
            this.submitted=false
        }
        console.log(this.form)
    }
   } 
}
</script>

<style>
</style>