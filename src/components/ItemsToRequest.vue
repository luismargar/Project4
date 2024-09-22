<script setup>
import { ref } from 'vue';

// Reactive variables
const itemName = ref('');
const itemsOnHand = ref(0);
const itemsRequired = ref(100); // Default requirement set to 100
const requestStatus = ref('');

const calculateItemsToRequest = () => {
  if (!itemName.value.trim()) {
    requestStatus.value = 'Please enter an item name.';
    return;
  }

  const shortage = itemsRequired.value - itemsOnHand.value;
  
  if (shortage > 0) {
    requestStatus.value = `You need to request ${shortage} more ${itemName.value}(s).`;
  } else if (shortage < 0) {
    requestStatus.value = `You have enough ${itemName.value}(s). No need to request more.`;
  } else {
    requestStatus.value = `You have exactly the required amount of ${itemName.value}(s).`;
  }
};
</script>

<template>
    <div class="items-to-request">
      <h1>Items To Request</h1>
      
      <input
        type="text"
        v-model="itemName"
        placeholder="Enter item name"
      />
      
      <input
        type="number"
        v-model="itemsOnHand"
        placeholder="Enter items on hand"
      />
      
      <input
        type="number"
        v-model="itemsRequired"
        placeholder="Enter items required"
      />
      
      <button @click="calculateItemsToRequest">Calculate Request</button>
      
      <p v-if="requestStatus">{{ requestStatus }}</p>
    </div>
  </template>