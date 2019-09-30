<template>
      <div class="home">
        <b-container >
          <b-row>
          <b-col>
              <h3><b>Shopping List</b></h3>
              <!-- item attribute helps you pass on data to itemTable because it starts with : 
              it does the same as v-bind -->
              <item-table :items= "items" @delete:item= "deleteItem" @edit:item= "editItem"  />
              
              <!-- OR
              <item-table v-bind:items="items" /> -->    
          </b-col>
          
          <b-col>
            <h3><b>Add Items to Shopping List</b></h3>
            <AddItemForm  @add:item= "addItem" /><br>
          </b-col>
          </b-row>
        </b-container > 
      </div>
</template>

<script>
import ItemTable from '@/components/ItemTable.vue'
import AddItemForm from '@/components/AddItemForm.vue'
export default {
  name: 'app',
  components: {
    ItemTable,
    AddItemForm,
  },
  data(){
    return{
      items: [
        {
          id: 1,
          name: 'Basket',
          quantity: 5,
          amount: 500,
        },
      ],
     
    }
  },
  methods:{
    /* 
    method to add items to the items array */
    addItem(item) {
    const lastId = 
        this.items.length > 0 
           ? this.items[this.items.length - 1].id
            : 0;
    const id = lastId + 1;
    const newItem = { ...item, id };
    this.items = [...this.items, newItem];
   
    // total = newItem + this.amount;
    }, 
    /* 
    creating method to delete an item from the items array */
    deleteItem(id){
      this.items = this.items.filter(
        employee => employee.id !== id
      )
    },
    /* 
    creating method to edit an item from the items array */
    editItem(id, updateItem){
      this.items = this.items.map(item => 
      item.id === id? updateItem : item)
    },
 

   },


}
</script>
<style>
.container{
  padding-bottom: 900px;
}

</style>
