<script setup>
import { ref } from 'vue';

const newItemName = ref('');
const newItemQuantity = ref(1);
const items = ref([]);

const addItem = () => {
  if (newItemName.value.trim() && newItemQuantity.value > 0) {
    items.value.push({
      name: newItemName.value.trim(),
      quantity: newItemQuantity.value,
    });
    newItemName.value = '';
    newItemQuantity.value = 1; // Reset quantity to default
  }
};
</script>

<template>
    <div class="inventory-tracker">
      <h1>Inventory Tracker</h1>
      
      <input
        type="text"
        v-model="newItemName"
        placeholder="Enter item name"
        @keyup.enter="addItem"
      />
      
      <input
        type="number"
        v-model="newItemQuantity"
        placeholder="Enter quantity"
        @keyup.enter="addItem"
      />
      
      <button @click="addItem">Add Item</button>
      
      <ul>
        <li v-for="(item, index) in items" :key="index">
          {{ item.name }} - {{ item.quantity }}
        </li>
      </ul>
    </div>
  </template>