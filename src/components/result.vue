<template>
  <!-- Result View -->
  <div v-if="showResult" class="mt-0">
    <!-- nav bar section -->
    <div class="flex justify-between items-center text-black">
      <div class="bg-gray-700 rounded">
        <img
          class="w-[200px] bg-gray-700"
          src="./assets/Black and Blue Mobile Phone Repair Logo.png"
          alt="LOGO"
        />
      </div>
      <div class="lg:mr-20 md:mr-20">
        <h1 class="font-bold text-[#0ace7cd8] text-[30px]">SALES</h1>
        <p class="font-bold text-[12px]">{{ data.month }} {{ data.day }}, {{ data.year }}</p>
      </div>
    </div>

    <div>
      <!-- hero section -->
      <div class="flex justify-between items-center text-black">
        <div class="ml-5 lg:ml-20 md:ml-20">
          <h1 class="font-bold text-[#0ace7cd8] text-[20px]">AWOOWE ELECTRONICS</h1>
          <p>Soobe, Abdishideeye, Somalia</p>
          <p>0619538337</p>
        </div>
        <div class="mr-5 lg:mr-20 md:mr-20">
          <h1 class="font-bold text-[#0ace7cd8] text-[17px]">BILL TO</h1>
          <p class="font-bold text-[#0ace7cd8] text-[14px]">{{ items[0]?.name }}</p>
          <p class="font-[400]">{{ items[0]?.number }}</p>
        </div>
      </div>
    </div>

    <!-- Items table -->
    <div class="mt-10 ml-5 mr-5">
      <table class="min-w-full border border-gray-300">
        <thead>
          <tr class="bg-teal-700 text-white text-left">
            <th class="px-2 py-1 border-r border-white">#</th>
            <th class="px-4 py-2 border-r border-white">Item Description</th>
            <th class="px-4 py-2 border-r border-white">Quantity</th>
            <th class="px-4 py-2 border-r">Price</th>
            <th class="px-4 py-2">Total</th>
          </tr>
        </thead>
        <tbody class="bg-white text-sm">
          <tr v-for="(item, index) in items" :key="index" class="border-b border-gray-300">
            <td class="px-2 py-1">{{ index + 1 }}</td>
            <td class="px-4 py-2 font-semibold">{{ item.description }}</td>
            <td class="px-4 py-2">{{ item.quantity }} PC</td>
            <td class="px-4 py-2">${{ item.price }}</td>
            <td class="px-4 py-2 text-green-700 font-semibold">${{ item.total.toFixed(2) }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- Payment Info and Summary -->
    <div class="flex justify-between lg:mx-10 md:mx-10 ml-2 mt-6 border-b-2 border-green-300">
      <div>
        <h1 class="font-bold text-[#0ace7cd8] text-[17px]">Payment Info</h1>
        <p>evc0619538337 / edhab 0629538337</p>

        <h1 class="font-bold text-[#0ace7cd8] text-[17px] mt-4">Served by</h1>
        <p>{{ items[0]?.served }}</p>

        <div>
          <img
            class="w-[200px]"
            src="./assets/Black and Blue Mobile Phone Repair Logo.png"
            alt="Logo"
          />
        </div>
      </div>

      <div class="w-full lg:w-auto md:w-auto sm:auto mb-4 mr-0">
        <div class="mb-[16px]">
          <span
            class="bg-teal-500 font-bold text-white text-[15px] py-2 ml-5 lg:pl-4 md:pl-4 pl-[5px] lg:pr-10 md:pr-10 pr-3"
          >
            TOTAL AMOUNT
          </span>
          <span
            class="inline-block bg-teal-400 font-bold text-white py-[6px] pl-4 w-[70px] lg:w-[140px] md:w-[140px]"
            >${{ totalPrice.toFixed(2) }}</span
          >
        </div>

        <div class="mb-[16px]">
          <span
            class="bg-teal-500 font-bold text-white text-[15px] py-2 ml-5 lg:pl-4 md:pl-4 pl-[5px] lg:pr-[82px] md:pr-[82px] pr-[50px]"
            >DISCOUNT</span
          >
          <span
            class="inline-block bg-teal-400 font-bold text-white py-[6px] pl-4 w-[70px] lg:w-[140px] md:w-[140px]"
            >${{ totalDiscount.toFixed(2) }}</span
          >
        </div>

        <div class="mb-[16px]">
          <span
            class="bg-teal-500 font-bold text-white text-[15px] py-2 ml-5 lg:pl-4 md:pl-4 pl-[5px] lg:pr-[123px] md:pr-[123px] pr-[91px]"
            >PAID</span
          >
          <span
            class="inline-block bg-teal-400 font-bold text-white py-[6px] pl-4 w-[70px] lg:w-[140px] md:w-[140px]"
            >${{ totalPaid.toFixed(2) }}</span
          >
        </div>

        <div>
          <span
            class="bg-teal-500 font-bold text-white text-[15px] py-2 ml-5 lg:pl-4 md:pl-4 pl-[5px] lg:pr-[90px] md:pr-[90px] pr-[57px]"
            >BALANCE</span
          >
          <span
            class="inline-block bg-teal-400 font-bold text-white py-[6px] pl-4 w-[70px] lg:w-[140px] md:w-[140px]"
            >${{ totalBalance.toFixed(2) }}</span
          >
        </div>
      </div>
    </div>

    <h1 class="font-bold text-green-700 mt-5 mb-20 ml-10">
      Thank you {{ items[0]?.name }} for the purchase
    </h1>

    <button
      class="print-button bg-blue-600 py-2 px-4 rounded ml-6 mb-6 text-white font-bold"
      @click="printReceipt"
    >
      Print Receipt
    </button>
  </div>

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
      <button class="bg-green-600 text-white py-2 px-4 rounded" @click="addItem">
        Add Item
      </button>

      <button class="bg-blue-600 text-white py-2 px-4 rounded" @click="submitForm">
        Submit All
      </button>
    </div>
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

      itemDescription: "",
      name: "",
      served: "",
      number: null,
      quantity: null,
      price: null,
      discount: 0,
      balance: null,
      paid: null,
      items: [],
      showResult: false,
    };
  },
  computed: {
    totalPrice() {
      // Sum of all items total
      return this.items.reduce((sum, item) => sum + item.total, 0);
    },
    totalDiscount() {
      return this.items.reduce((sum, item) => sum + (item.discount || 0), 0);
    },
    totalPaid() {
      return this.items.reduce((sum, item) => sum + (item.paid || 0), 0);
    },
    totalBalance() {
      return this.items.reduce((sum, item) => sum + (item.balance || 0), 0);
    },
  },
  methods: {
    addItem() {
      if (
        !this.itemDescription ||
        this.quantity <= 0 ||
        this.price <= 0
      ) {
        alert("Please fill all fields correctly.");
        return;
      }

      const total = (this.quantity * this.price) - (this.discount || 0);

      const item = {
        description: this.itemDescription,
        quantity: this.quantity,
        price: this.price,
        discount: this.discount || 0,
        paid: this.paid || 0,
        balance: this.balance || 0,
        name: this.name,
        served: this.served,
        total: total >= 0 ? total : 0,
        number: this.number,
      };

      this.items.push(item);

      // clear form
      this.itemDescription = "";
      this.quantity = null;
      this.price = null;
      this.discount = 0;
      this.paid = null;
      this.balance = null;
      // NOTE: Keep name, number, served as is so user doesn't retype each item
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
      this.name = "";
      this.number = null;
      this.served = "";
    },
    printReceipt() {
      window.print();
    },
  },
};
</script>
