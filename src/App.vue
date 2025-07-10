<template>
  <!-- Result View -->
  <result
    v-if="showResult"
    :items="items"
    @go-back="clearform"
  />
  

  <!-- Form View -->
  <div v-else class="flex flex-col justify-center items-center h-screen gap-3">

    <input
      v-model="name"
      type="text"
      placeholder="Customer Name"
      class="p-2 border rounded w-64"
    />

    <input
      v-model="number"
      type="number"
      placeholder="Customer Number"
      class="p-2 border rounded w-64"
    />

    <input
      v-model="served"
      type="text"
      placeholder="Served by"
      class="p-2 border rounded w-64"
    />

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

    <input
      v-model.number="discount"
      type="number"
      placeholder="Discount"
      class="p-2 border rounded w-64"
    />
    <input
      v-model.number="paid"
      type="number"
      placeholder="Paid"
      class="p-2 border rounded w-64"
    />
    <input
      v-model.number="balance"
      type="number"
      placeholder="Balance"
      class="p-2 border rounded w-64"
    />

    <div class="flex gap-4 mt-4">
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
      name: '',
      served: '',
      number: null,
      quantity: null,
      price: null,
      discount: null,
      balance: null,
      paid: null,
      subtotal: null,
      tax: null,
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
        discount: this.paid - this.discount,
        paid: this.paid,
        balance: this.balance,
        name: this.name,
        served: this.served,
        total: this.quantity * this.price,
        number: this.number,
      };

      this.items.push(item);

      // clear form
      this.itemDescription = '';
      this.name = '';
      this.quantity = null;
      this.price = null;
      this.price = null;
      this.discount = null;
      this.subtotal = null;
      this.tax = null;
      this.balance = null;
      this.paid = null;
      this.number = null;
      this.served = '';
    },
    submitForm() {
      if (this.items.length === 0) {
        alert("Please add at least one item before submitting.");
        return;
      }
      this.showResult = true;
    },
    clearform() {
       this.items = [];
      this.showResult = false;
    }
  },
  };
</script>
