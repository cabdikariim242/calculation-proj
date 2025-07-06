<template>
  <div class="p-6 max-w-md mx-auto space-y-4">
    <!-- Inputs -->
    <input
      v-model="description"
      type="text"
      placeholder="Item Description"
      class="border p-2 rounded w-full"
    />
    <input
      v-model.number="quantity"
      type="number"
      placeholder="Quantity"
      class="border p-2 rounded w-full"
    />
    <input
      v-model.number="price"
      type="number"
      placeholder="Price"
      class="border p-2 rounded w-full"
    />

    <!-- Add Button -->
    <button @click="addItem" class="bg-blue-600 text-white px-4 py-2 rounded">
      Add Item
    </button>

    <!-- Items List -->
    <div v-for="(item, index) in items" :key="index" class="border p-2 rounded bg-gray-50 flex gap-10">
      <p>
        <span>Quantity:</span>
        <strong>{{ item.description }}</strong></p>

      <p>
        <span>Quantity:</span>
        {{ item.quantity }}
      </p>
      <p>
        <span>Price:</span>
        ${{ item.price }}
      </p>
    </div>

    <!-- Total -->
    <p class="text-xl font-bold mt-4">Total Price: ${{ total }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      description: '',
      quantity: 0,
      price: 0,
      items: [],
      total: 0
    };
  },
  methods: {
    addItem() {
      if (!this.description || this.price <= 0) {
        alert('Please enter a valid description and price.');
        return;
      }

      const newItem = {
        description: this.description,
        quantity: this.quantity,
        price: this.price
      };

      this.items.push(newItem);

      // clear inputs
      this.description = '';
      this.quantity = 0;
      this.price = 0;

      // update total
      this.updateTotal();
    },

    updateTotal() {
      this.total = this.items.reduce((sum, item) => sum + item.price, 0);
    }
  }
};
</script>

