<template>
  <!-- Result View -->
  <result
    v-if="showResult"
    :items="items"
    @go-back="showResult = false"
  />

  <!-- Form View -->
  <div v-else class="flex flex-col justify-center items-center h-screen gap-3">
    <input
      v-model="itemDescription"
      type="text"
      placeholder="Item Description"
      class="p-2 border rounded w-64"
    />
    <input
      v-model.number="quantity"
      type="number"
      placeholder="Quantity"
      class="p-2 border rounded w-64"
    />
    <input
      v-model.number="price"
      type="number"
      placeholder="Price"
      class="p-2 border rounded w-64"
    />

    <button
      class="bg-green-600 text-white py-2 px-4 rounded"
      @click="addItem"
    >
      Add Item
    </button>

    <button
      class="bg-blue-600 text-white py-2 px-4 rounded"
      @click="submitForm"
    >
       Submit All
    </button>
  </div>
</template>

<script>
import result from './components/result.vue';

export default {
  name: 'App',
  components: { result },
  data() {
    return {
      itemDescription: '',
      quantity: '',
      price: null,
      items: [],
      showResult: false,
    };
  },
  methods: {
    addItem() {
      if (!this.itemDescription || this.quantity <= 0 || this.price <= 0) {
        alert("Please fill all fields correctly.");
        return;
      }

      const item = {
        description: this.itemDescription,
        quantity: this.quantity,
        price: this.price,
        total: this.quantity * this.price,
      };

      this.items.push(item);

      // clear form
      this.itemDescription = '';
      this.quantity = 0;
      this.price = 0;
    },
    submitForm() {
      if (this.items.length === 0) {
        alert("Please add at least one item before submitting.");
        return;
      }
      this.showResult = true;
    }
  }
};
</script>
