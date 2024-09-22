<script setup>
import { ref, onMounted } from 'vue';
import Header from './components/Header.vue';
import ItemsOnHand from './components/ItemsOnHand.vue';
import ItemsRequired from './components/ItemsRequired.vue';
import ItemsToRequest from './components/ItemsToRequest.vue';

const items = ref([]);

const saveToLocalStorage = () => {
  localStorage.setItem('inventoryItems', JSON.stringify(items.value));
};

onMounted(() => {
  const storedItems = localStorage.getItem('inventoryItems');
  if (storedItems) {
    items.value = JSON.parse(storedItems);
  }
});

defineExpose({ items, saveToLocalStorage });
</script>

<template>
  <Header></Header>
  <ItemsOnHand :items="items" @save="saveToLocalStorage"></ItemsOnHand>
  <ItemsRequired></ItemsRequired>
  <ItemsToRequest></ItemsToRequest>

</template>