<script setup>
import { ref, watch } from 'vue';

const props = defineProps(['items']);
const emit = defineEmits();

const newItemName = ref('');
const newItemQuantity = ref(1);

const addItem = () => {
  if (newItemName.value.trim() && newItemQuantity.value > 0) {
    props.items.push({
      name: newItemName.value.trim(),
      quantity: newItemQuantity.value,
    });
    newItemName.value = '';
    newItemQuantity.value = 1; 

    emit('save');
  }
};

const deleteItem = (index) => {
  props.items.splice(index, 1);
  emit('save');
};

watch(() => props.items, () => {
  emit('save');
}, { deep: true });
</script>

<template>
  <div class="items-on-hand">
    <h1>Items On Hand</h1>
    
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
        <button @click="deleteItem(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>
