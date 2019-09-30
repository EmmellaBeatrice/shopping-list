<template>
<!-- creating a form for adding item and their quantities into our shopping list -->
    <div id="item-form">
        <!-- the prevent helps in preventing the default GET/POST -->
        <b-form inline @submit.prevent="handleSubmit" id="myform">
            
              <label for="item-name"><b>Item</b></label>&nbsp; 
                <b-form-input 
                ref="first"
                v-model= "item.name" 
                type= "text" 
                class= "{ 'has-error': submitting && invalidName} form-control" 
                placeholder= "Bottle" 
                @focus= "clearStatus"
                @keypress= "clearStatus"
                />&nbsp; 
                <label for="quantity"><b>Quantity</b></label>&nbsp; 
                <b-form-input 
                v-model="item.quantity"
                type="text" 
                class="{'has-error': submitting && invalidName} form-control" 
                placeholder="2" 
                @focus= "clearStatus"/>&nbsp; 
                <label for="amount"><b>Amount</b></label>&nbsp; 
                <b-form-input 
                v-model="item.amount"
                type="text" 
                class="{'has-error': submitting && invalidName} form-control" 
                placeholder="UGX   2000" 
                @focus= "clearStatus"/>&nbsp; &nbsp; 
                <button class="btn btn-primary">Add Item</button>
                <span v-if= "error && submitting" class= "error-message">
                    Please fill in all fields, Quantity and Amount must be a number
                </span>
                <span v-if= "success" class="success-message">
                    Item Added Successfully
                </span>
        </b-form>
        
    </div>
</template>
<script>
export default {
    name: 'item-form',
    //will recieve props inform of an array
        data() {
        return{
            /* Adding submiting state to check whether the form is currently being submitted, 
            An error state if something went wrong, and a success state  if it went well */
            submitting: false,
            error: false,
            success: false,
            item: {
                name: '',
                quantity: '',
                amount: '',
            },

        }
    },
    methods: {
            /* 
            creating submit function which will first clear whether success/error are set,
            check our computed properties and if true an error will be set 
            or if not we can submit and set all the states back to default.
            */
        handleSubmit(){
            // console.log('testing handle submit')
            this.submitting = true
            this.clearStatus()

            if (this.invalidItem || this.invalidQuantity || this.invalidAmount){
                this.error = true
                return
            }
            /* 
            passing items from the form to the table or to parent */
            this.$emit(
                //name of event to emit
                'add:item',
                //data to pass
                this.item
            )
            this.$refs.first.focus()
            this.item = {
                name: '',
                quantity: '',
                amount: '',
            }
            this.error = false
            this.success = true
            this.submitting = false
        },
        clearStatus() {
            this.success = false
            this.error = false
        }
    },
    //checking whether fields are empty
    computed: {
        invalidItem() {
            return this.item.name === ''
        },
        invalidQuantity() {
            if (this.item.quantity === '' || isNaN(this.item.quantity) )
            return true
        },
        invalidAmount(){
            return isNaN(this.item.amount)
        }
    },
}
</script>
<style>
#myform{
  padding-left: 15px;
}
[class*='-message']{
   font-weight: 900; 
}
.error-message{
    color: #d33c40;
}
.success-message{
    color: #32a95d;
}
</style>

