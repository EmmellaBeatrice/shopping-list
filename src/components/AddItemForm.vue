<template>
<!-- creating a form for adding item and their quantities into our shopping list -->
    <div id="item-form">
        <!-- the prevent helps in preventing the default GET/POST -->
        <form @submit.prevent="handleSubmit" id="myform" >
            <div class="form-group row">
                <label for="item-name"><b>Item</b></label>
                <input 
                ref="first"
                v-model= "item.name" 
                type= "text" 
                class= "{ 'has-error': submitting && invalidName} form-control" 
                placeholder= "Bottle" 
                @focus= "clearStatus"
                @keypress= "clearStatus"
                />
            </div>
            <div class="form-group row">
                <label for="quantity"><b>Quantity</b></label>
                <input 
                v-model="item.quantity"
                type="text" 
                class="{'has-error': submitting && invalidName} form-control" 
                placeholder="2" 
                @focus= "clearStatus"/>
                <p v-if= "error && submitting" class= "error-message">
                    Please fill in all fields
                </p>
                <p v-if= "success" class="success-message">
                    Item Successfully added
                </p>
            </div>
                <button class="btn btn-primary">Add Item</button>

            
        </form>
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

            if (this.invalidItem || this.invalidQuantity){
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
            
            return
        },
    },
}
</script>
<style>
#myform{
  padding-left: 15px;
}
[class*='-message']{
   font-weight: 500; 
}
.error-message{
    color: #d33c40;
}
.success-message{
    color: #32a95d;
}
</style>

