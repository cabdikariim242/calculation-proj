<!-- <template>
  <nav>
    <router-link to="/">Home</router-link>
    <router-link :to="{ name: 'about' }">About</router-link>
  </nav>
  <!-- <div class="flex justify-center items-center flex-col h-screen">
    <input
      class="border-2 border-gray-800 p-2 rounded"
      type="text"
      v-model="itemsDescription"
      placeholder="Search..."
      required
    />
    <input
      class="border-2 border-gray-800 p-2 rounded"
      type="text"
      v-model="Quantity"
      placeholder="Search..."
      required
    />
    <input
      class="border-2 border-gray-800 p-2 rounded"
      type="number"
      v-model="price"
      placeholder="Search..."
      required
    />
    
   


    <button class="bg-blue-500 text-white p-2 rounded mt-3" @click="addInput">add input</button>
   
   <div  v-for="item in items " :key="items" class="mt-2">
  
   </div>
   <p> item Description -{{ itemsDescription }} -- Quantity -- {{ Quantity }} the price {{ price }} -- the total is {{ total }} </p>
  </div> -->
<!-- </template> -->
<!-- 
<script>
export default {
  data() {
    return {
      totalnum: 0,
      price: 0,
      Quantity: '',
      itemsDescription: "",
      items: [{
        'itemsDescription':'',  'Quantity': '', 'price': 0, 'total': 0
      }],
      total: 0 ,
    };
  },
  methods: {
      addInput() {
        if (this.itemsDescription && this.Quantity && this.price) {
          const total = Number(this.Quantity) * Number(this.price);
          this.items.push({
            itemsDescription: this.itemsDescription,
            Quantity: this.Quantity,
            price: this.price,
            total: total
          });
          this.total = total;
          this.itemsDescription = '';
          this.Quantity = '';
          this.price = 0;
        }
      }
    }
  };
</script> --> 

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

