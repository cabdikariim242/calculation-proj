<template>
  <div class="min-h-screen bg-gray-50 p-4 sm:p-8">
    <!-- Show product management & form only when NOT showing result -->
    <template v-if="!showResult">
      <!-- Product Management Panel -->
      <section class="max-w-4xl mx-auto mb-12 bg-white p-6 rounded-lg shadow-md">
        <h2 class="text-2xl font-bold mb-4 text-teal-700">Product Management</h2>
        <div class="flex flex-col sm:flex-row sm:items-center gap-4">
          <input
            v-model="newProductName"
            type="text"
            placeholder="New product name"
            class="border p-2 rounded flex-grow"
          />
          <input
            v-model.number="newProductPrice"
            type="number"
            min="0"
            placeholder="Price"
            class="border p-2 rounded w-28"
          />
          <button
            @click="addProduct"
            class="bg-teal-600 text-white px-4 py-2 rounded hover:bg-teal-700 transition"
          >
            Add Product
          </button>
        </div>

        <ul class="mt-6 space-y-2 max-h-40 overflow-auto">
          <li
            v-for="(product, index) in products"
            :key="product.name"
            class="flex justify-between items-center border-b py-2 gap-2"
          >
            <template v-if="editIndex === index">
              <input
                v-model="editName"
                type="text"
                class="border p-1 rounded flex-grow"
              />
              <input
                v-model.number="editPrice"
                type="number"
                min="0"
                class="border p-1 rounded w-24"
              />
              <button
                @click="saveEdit(index)"
                class="bg-green-600 text-white px-3 py-1 rounded hover:bg-green-700 transition"
              >
                Save
              </button>
              <button
                @click="cancelEdit"
                class="bg-gray-400 text-white px-3 py-1 rounded hover:bg-gray-500 transition"
              >
                Cancel
              </button>
            </template>

            <template v-else>
              <span class="font-semibold text-gray-700 flex-grow">{{ product.name }}</span>
              <span class="font-semibold text-teal-700 w-20 text-right">${{ product.price.toFixed(2) }}</span>
              <button
                @click="startEdit(index)"
                class="bg-yellow-400 text-white px-3 py-1 rounded hover:bg-yellow-500 transition ml-4"
              >
                Edit
              </button>
              <button
                @click="deleteProduct(index)"
                class="bg-red-600 text-white px-3 py-1 rounded hover:bg-red-700 transition ml-2"
              >
                Delete
              </button>
            </template>
          </li>
        </ul>
      </section>

      <!-- Sales Form -->
      <section class="max-w-4xl mx-auto bg-white p-6 rounded-lg shadow-md">
        <h2 class="text-2xl font-bold mb-4 text-teal-700">Sales Form</h2>

        <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 mb-4">
          <input
            v-model="name"
            type="text"
            placeholder="Customer Name"
            class="p-2 border rounded w-full"
          />
          <input
            v-model="number"
            type="number"
            placeholder="Customer Number"
            class="p-2 border rounded w-full"
          />
          <input
            v-model="served"
            type="text"
            placeholder="Served by"
            class="p-2 border rounded w-full"
          />
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-4 gap-4 mb-6 items-end">
          <select
            v-model="selectedItemName"
            @change="onSelectItem"
            class="p-2 border rounded w-full"
          >
            <option value="" disabled>Select Item</option>
            <option
              v-for="item in products"
              :key="item.name"
              :value="item.name"
            >
              {{ item.name }}
            </option>
          </select>

          <input
            v-model.number="price"
            type="number"
            placeholder="Price"
            readonly
            class="p-2 border rounded w-full bg-gray-100 cursor-not-allowed"
          />

          <input
            v-model.number="quantity"
            type="number"
            min="1"
            placeholder="Quantity"
            class="p-2 border rounded w-full"
          />

          <input
            v-model.number="discount"
            type="number"
            min="0"
            placeholder="Discount (for this item)"
            class="p-2 border rounded w-full"
          />
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 mb-6">
          <input
            v-model.number="paid"
            type="number"
            min="0"
            placeholder="Paid (total)"
            class="p-2 border rounded w-full"
          />
          <input
            v-model.number="balance"
            type="number"
            min="0"
            placeholder="Balance (total)"
            class="p-2 border rounded w-full"
          />
        </div>

        <div class="flex gap-4">
          <button
            @click="addItem"
            class="bg-green-600 text-white py-2 px-4 rounded hover:bg-green-700 transition"
          >
            Add Item
          </button>

          <button
            @click="submitForm"
            class="bg-blue-600 text-white py-2 px-4 rounded hover:bg-blue-700 transition"
          >
            Submit All
          </button>
        </div>
      </section>
    </template>

    <!-- Result View -->
    <section
      v-if="showResult"
      class="max-w-4xl mx-auto bg-white p-6 rounded-lg shadow-md"
    >
      <div class="flex flex-col justify-center items-center mb-6">
        <img
          class="w-48 mb-4"
          src="./assets/Black and Blue Mobile Phone Repair Logo.png"
          alt="Logo"
        />
        <div class="text-center">
          <h1 class="text-4xl font-bold text-teal-700 tracking-wide">SALES</h1>
          <p class="font-semibold text-gray-600 text-lg mt-1">
            {{ data.month }} {{ data.day }}, {{ data.year }}
          </p>
        </div>
      </div>

      <div class="mb-6 text-center text-gray-800 space-y-2">
        <div>
          <h2 class="text-2xl font-bold text-teal-700">AWOOWE ELECTRONICS</h2>
          <p class="text-lg">Soobe, Abdishideeye, Somalia</p>
          <p class="text-lg">0619538337</p>
        </div>
        <div>
          <h3 class="text-xl font-semibold text-teal-700 mt-4">BILL TO</h3>
          <p class="font-semibold text-gray-700 text-lg">{{ items[0]?.name }}</p>
          <p class="text-lg">{{ items[0]?.number }}</p>
        </div>
      </div>

      <div class="overflow-x-auto mb-6">
        <table class="min-w-full border border-gray-300 rounded-lg overflow-hidden">
          <thead class="bg-teal-700 text-white">
            <tr>
              <th class="px-3 py-2 text-left">#</th>
              <th class="px-4 py-2 text-left">Item Description</th>
              <th class="px-4 py-2 text-left">Quantity</th>
              <th class="px-4 py-2 text-left">Price</th>
              <th class="px-4 py-2 text-left">Discount</th>
              <th class="px-4 py-2 text-left">Total</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(item, index) in items"
              :key="index"
              class="border-b border-gray-300 hover:bg-gray-100"
            >
              <td class="px-3 py-2">{{ index + 1 }}</td>
              <td class="px-4 py-2 font-semibold">{{ item.description }}</td>
              <td class="px-4 py-2 text-[gray] text-[16px]">{{ item.quantity }} {{ item.description }}</td>
              <td class="px-4 py-2">${{ item.price.toFixed(2) }}</td>
              <td class="px-4 py-2 text-red-600">-${{ item.discount.toFixed(2) }}</td>
              <td class="px-4 py-2 font-semibold text-green-700">${{ item.total.toFixed(2) }}</td>
            </tr>
          </tbody>
        </table>
      </div>

      <div
        class="flex flex-col justify-center items-center space-y-2 text-gray-700 font-semibold text-lg"
      >
        <div class="flex justify-between w-full max-w-xs">
          <span>Total Amount:</span>
          <span>${{ totalPrice.toFixed(2) }}</span>
        </div>

        <div class="flex justify-between w-full max-w-xs">
          <span>Total Discount:</span>
          <span>-${{ totalDiscount.toFixed(2) }}</span>
        </div>

        <div class="flex justify-between w-full max-w-xs">
          <span>Paid:</span>
          <span>${{ paid || 0 }}</span>
        </div>

        <div class="flex justify-between w-full max-w-xs">
          <span>Balance:</span>
          <span>${{ balance || 0 }}</span>
        </div>
      </div>

      <h2 class="mt-8 text-green-700 font-bold text-xl text-center">
        Thank you {{ items[0]?.name }} for the purchase!
      </h2>

      <div class="flex justify-center mt-6">
        <button
          @click="printReceipt"
          class="bg-blue-600 text-white py-2 px-6 rounded hover:bg-blue-700 transition"
        >
          Print Receipt
        </button>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    const today = new Date();
    return {
      data: {
        month: today.toLocaleString("default", { month: "long" }),
        day: today.getDate(),
        year: today.getFullYear(),
      },

      // Customer & form data
      name: "",
      number: null,
      served: "",
      selectedItemName: "",
      price: 0,
      quantity: null,
      discount: null, // discount for current item
      paid: null, // total paid
      balance: null, // total balance

      // Product management
      products: [
        { name: "Screen Replacement", price: 50 },
        { name: "Battery Replacement", price: 30 },
        { name: "Charging Port Repair", price: 40 },
        { name: "Camera Repair", price: 60 },
        { name: "Software Update", price: 20 },
        { name: "Speaker Repair", price: 35 },
        { name: "Water Damage Fix", price: 80 },
        { name: "Button Repair", price: 25 },
      ],
      newProductName: "",
      newProductPrice: null,

      // Editing product state
      editIndex: null,
      editName: "",
      editPrice: null,

      // Items array & view state
      items: [],
      showResult: false,
    };
  },
  computed: {
    totalPrice() {
      return this.items.reduce((sum, item) => sum + item.total, 0);
    },
    totalDiscount() {
      return this.items.reduce((sum, item) => sum + (item.discount || 0), 0);
    },
  },
  methods: {
    onSelectItem() {
      const selectedProduct = this.products.find(
        (p) => p.name === this.selectedItemName
      );
      if (selectedProduct) {
        this.price = selectedProduct.price;
      } else {
        this.price = 0;
      }
    },
    addProduct() {
      if (
        !this.newProductName.trim() ||
        !this.newProductPrice ||
        this.newProductPrice <= 0
      ) {
        alert("Please enter a valid product name and price.");
        return;
      }

      if (
        this.products.some(
          (p) => p.name.toLowerCase() === this.newProductName.toLowerCase()
        )
      ) {
        alert("Product with this name already exists.");
        return;
      }

      this.products.push({
        name: this.newProductName.trim(),
        price: this.newProductPrice,
      });

      this.newProductName = "";
      this.newProductPrice = null;
    },
    startEdit(index) {
      this.editIndex = index;
      this.editName = this.products[index].name;
      this.editPrice = this.products[index].price;
    },
    cancelEdit() {
      this.editIndex = null;
      this.editName = "";
      this.editPrice = null;
    },
    saveEdit(index) {
      if (!this.editName.trim() || !this.editPrice || this.editPrice <= 0) {
        alert("Please enter valid name and price.");
        return;
      }

      // Check duplicate except for current editing product
      if (
        this.products.some(
          (p, i) =>
            i !== index && p.name.toLowerCase() === this.editName.toLowerCase()
        )
      ) {
        alert("Another product with this name already exists.");
        return;
      }

      this.products[index].name = this.editName.trim();
      this.products[index].price = this.editPrice;
      this.cancelEdit();

      // If the edited product is currently selected in form, update the price
      if (this.selectedItemName === this.products[index].name) {
        this.price = this.products[index].price;
      }
    },
    deleteProduct(index) {
      if (
        confirm(
          `Are you sure you want to delete the product "${this.products[index].name}"?`
        )
      ) {
        this.products.splice(index, 1);

        if (this.selectedItemName === this.products[index]?.name) {
          this.selectedItemName = "";
          this.price = 0;
        }
      }
    },
    addItem() {
      if (
        !this.selectedItemName ||
        this.quantity <= 0 ||
        this.price <= 0
      ) {
        alert("Please select an item and enter a valid quantity.");
        return;
      }

      const total = this.quantity * this.price - (this.discount || 0);

      this.items.push({
        description: this.selectedItemName,
        quantity: this.quantity,
        price: this.price,
        discount: this.discount || 0,
        total: total >= 0 ? total : 0,
        name: this.name,
        served: this.served,
        number: this.number,
      });

      this.selectedItemName = "";
      this.price = 0;
      this.quantity = null;
      this.discount = null;
    },
    submitForm() {
      if (this.items.length === 0) {
        alert("Please add at least one item before submitting.");
        return;
      }
      if (this.paid === null || this.balance === null) {
        alert("Please enter paid and balance amounts.");
        return;
      }
      this.showResult = true;
    },
    printReceipt() {
      window.print();
    },
  },
};
</script>

<style>
@media print {
  body * {
    visibility: hidden;
  }
  #app,
  #app * {
    visibility: visible;
  }
  #app {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
  }
}
</style>
