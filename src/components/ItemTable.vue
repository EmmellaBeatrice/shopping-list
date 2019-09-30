<template>
    <div id="item-table">
        <p v-if="items.length < 1" class="empty-table"> 
            No Items
        </p>
        <!-- Creating a table that displays items added through the form,
        the items in the table can be edited and deleted -->
        <table class="table table-bordered table-striped" v-else>
            <thead class="thead-dark">
                <tr>
                    <th>No</th>
                    <th>Item</th>
                    <th>Quantity</th>
                    <th>Price@</th>
                    <th>Actions</th>
                    <th>#</th>
                </tr>
            </thead>
            <tbody v-for="item in items" :key="item.id">
                <tr>
                    <td>{{ item.id }}</td>
                    <td v-if= "editing === item.id" >
                        <input type="text" v-model="item.name">
                    </td>
                    <td v-else>{{ item.name }}</td>
                    <td v-if= "editing === item.id">
                        <input type="text" v-model="item.quantity">
                    </td>
                    <td v-else>{{ item.quantity }}</td>                   
                    <td v-if= "editing === item.id">
                        <input type="text" v-model="item.amount">
                    </td>
                    <td v-else >{{ item.amount }}</td>
                    <td v-if="editing === item.id">
                        <button @click="editItem(item)">Save</button>
                        <button class="muted-button" @click="editing = null">Cancel</button>
                    </td>
                    <td v-else>
                        <button @click="editMode(item.id)">Edit</button> 
                        <button @click="$emit('delete:item', item.id)">Delete</button>
                    </td>
                    <td>
                        <input type="checkbox" v-model="selected" :value="item">
                    </td>
                    
                </tr>
        
            </tbody>
        </table>
        <strong>Total:  </strong><span>{{ total }}</span>
    </div>
</template>
<script>
export default {
    name: 'item-table',
    //telling the component that it will recieve data inform of an array
    props: {
        items: Array,
    },
    data() {
        return {
            editing: null,
            selected: [],
            
        }

        
    },
    methods: {
        /* creating an editing state that gets the id of the row currently being edited
        when edit mode is enabled
        */
        editMode(id){
            this.editing = id
        },
        editItem(item) {
            if (item.name ===  '' || item ===  '') return
            this.$emit('edit:item', item.id, item)
            this.editing = null
        },

    },
    computed: {
        total(){
            return this.selected.reduce(function (sum, item){
                return sum + parseInt(item.TOTAL) 
            }, 0)
        }
       },
}
</script>
<style>
#item-table {
padding-left: 0px;
}
</style>
