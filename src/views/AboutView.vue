<template>
  <div class="about">
    <input
      type="number"
      v-model="totalnum"
      placeholder="Enter total number"
      class="border-2 border-gray-800 p-2 rounded"
    />

    <div v-for="item in items" :key="item">
      <p>totalnum: {{ item.totalnum }}</p>
      <p>price: {{ item.price }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      totalnum: 0,
      
      items: ['price: 0',]
    };
  },
 
};
</script>
