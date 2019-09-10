<template>
    <div id="item-form">
        <!-- the prevent helps in preventing the default GET/POST -->
        <form @submit.prevent="handleSubmit" id="myform" >
            <div class="form-group row">
                <label for="item-name"><b>Item</b></label>
                <!-- v-model for two way data binding -->
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
            //Adding submiting state to check whether the form is currently being submitted, 
            //An error state if something went wrong, and a success state  if something when through properly
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
        handleSubmit(){
            // console.log('testing handle submit')
            /* 
            the submit function will first clear whether success/error then check our computed properties
            if true an error will be set if not we can submit and set all the statuses to default.
            */
            this.submitting = true
            this.clearStatus()

            if (this.invalidItem || this.invalidQuantity){
                this.error = true
                return
            }
            this.$emit(
                //name of emited event
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
            return this.item.quantity === ''
        },
    },
}
</script>
<style>
#myform{
  padding-left: 400px;
  padding-right: 500px;
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

