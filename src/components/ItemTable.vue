<template>
    <div id="item-table">
        <p v-if="items.length < 1" class="empty-table"> 
            No Items
        </p>
        <table class="table" v-else>
            <thead class="thead-dark">
                <tr>
                    <th>Item</th>
                    <th>Quantity</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <!-- retrieving items in the itemsTable and displaying it in the table-->
                <tr v-for="item in items" :key="item.id">
                    <td>{{ item.name }}</td>
                    <td>{{ item.quantity }}</td>
                    <td>
                        <button>Edit</button> 
                        <button @click="$emit('delete:item', item.id)">Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
export default {
    name: 'item-table',
    //telling the component that it will recieve data inform of an array
    props: {
        items: Array,
    }
}
</script>
<style>
#item-table {
padding-left: 300px;
padding-right: 300px;
padding-bottom: 65px;
}
</style>
