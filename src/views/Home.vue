<template>
  <div class="home">
    <h3><b>Add Items to shopping list</b></h3>
      <AddItemForm  @add:item= "addItem" /><br>
      
      <h3><b>Shopping List</b></h3>
      <!-- item attribute helps you pass on data to itemTable because it starts with : 
      it does the same as v-bind -->
      <item-table :items= "items" @delete:item= "deleteItem" @edit:item= "editItem" />
      <!-- OR
      <item-table v-bind:items="items" /> -->
       
  </div>
</template>

<script>
// @ is an alias to /src
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
          quantity: '5',
        },
       
      ],
    }
  },
   methods:{
    // method to modify the items list array
    addItem(item) {
    const lastId = 
        this.items.length > 0 
           ? this.items[this.items.length - 1].id
            : 0;
    const id = lastId + 1;
    const newItem = { ...item, id };
    this.items = [...this.items, newItem];
    }, 
    //creating method to delete an item from the item list array
    deleteItem(id){
      this.items = this.items.filter(
        employee => employee.id !== id
      )
    },
    editItem(id, updateItem){
      this.items = this.items.map(item => 
      item.id === id? updateItem : item)
    }
   }

}
</script>
<style>
  h3 {
    text-align: left;
    padding-left: 300px;
  }

</style>
