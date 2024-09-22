<script setup>
import { ref } from 'vue';

const constantValue = 100;

const itemName = ref('');
const requiredQuantity = ref(0);
const requirementStatus = ref('');

const checkRequirement = () => {
  if (!itemName.value.trim()) {
    requirementStatus.value = 'Please enter an item name.';
    return;
  }
  
  if (requiredQuantity.value > constantValue) {
    requirementStatus.value = `For ${itemName.value}, you need more than 100 items.`;
  } else if (requiredQuantity.value < constantValue) {
    requirementStatus.value = `For ${itemName.value}, you have less than 100 items.`;
  } else {
    requirementStatus.value = `You have exactly 100 items for ${itemName.value}.`;
  }
};
</script>

<template>
    <div class="items-required">
      <h1>Items Required</h1>
      
      <input
        type="text"
        v-model="itemName"
        placeholder="Enter item name"
      />
      
      <input
        type="number"
        v-model="requiredQuantity"
        placeholder="Enter required quantity"
      />
      
      <button @click="checkRequirement">Check Requirement</button>
      
      <p v-if="requirementStatus">{{ requirementStatus }}</p>
    </div>
  </template>