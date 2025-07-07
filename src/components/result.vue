<template>
  <div class="p-6 max-w-md mx-auto bg-gray-100 rounded shadow">
    <h2 class="text-xl font-bold mb-4">Submitted Items</h2>

    <ul v-if="items.length" class="space-y-3">
      <li
        v-for="(item, index) in items"
        :key="index"
        class="border-b pb-2"
      >
        <p><strong>Description:</strong> {{ item.description }}</p>
        <p><strong>Quantity:</strong> {{ item.quantity }} PC</p>
        <p><strong>Price:</strong> ${{ item.price }}</p>
        <p><strong>Total:</strong> ${{ item.total }}</p>
      </li>
    </ul>

    <!-- Grand Total -->
    <p class="mt-4 font-bold text-green-700 text-lg">
      Grand Total: ${{ totalPrice }}
    </p>

    <button
      @click="$emit('go-back')"
      class="mt-6 bg-red-500 text-white px-4 py-2 rounded"
    >
       Go Back
    </button>
  </div>
</template>

<script>
export default {
  name: 'Result',
  props: {
    items: {
      type: Array,
      required: true
    }
  },
  computed: {
    totalPrice() {
      return this.items.reduce((sum, item) => sum + item.total, 0);
    }
  }
};
</script>
