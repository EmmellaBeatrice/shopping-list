<template>
  <div class="add-item">
    <!-- displaying the form -->
      <AddItemForm  @add:item= "addItem" />
  </div>
</template>

<script>
import AddItemForm from '@/components/AddItemForm.vue'
export default {
  name: 'app',
  components: {
    AddItemForm,
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

  },

}
</script>