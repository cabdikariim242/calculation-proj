<template>
  <div class="mt-0">
    <!-- nav bar section -->
    <div class="flex justify-between items-center text-black">
      <div class="bg-gray-700 rounded">
        <img
          class="w-[200px] bg-gray-700"
          src="../assets/Black and Blue Mobile Phone Repair Logo.png"
          alt="LOGO"
        />
      </div>
      <div class=" lg:mr-20 md:mr-20">
        <h1 class="font-bold text-[#0ace7cd8] text-[30px]">SALES</h1>
        <P class="font-bold text-[12px]">{{data.month}} {{data.day}}, {{data.year}}</P>
      </div>
    </div>
    <div>
      <!-- hero section -->

      <div class="flex justify-between items-center text-black">
        <div class="ml-5 lg:ml-20 md:ml-20">
          <h1 class="font-bold text-[#0ace7cd8] text-[20px]">
            AWOOWE ELECTRONICS
          </h1>
          <p>Soobe, Abdishideeye, somalia</p>
          <p>0619538337</p>
        </div>
        <div class="mr-5 lg:mr-20 md:mr-20">
          <h1 class="font-bold text-[#0ace7cd8] text-[17px]">BILL TO</h1>
          <p class="font-bold text-[#0ace7cd8] text-[14px]">{{items[0]?.name}}</p>
          <p class="font-[400]">{{items[0]?.number}}</p>
        </div>
      </div>
    </div>

    <!-- third section -->
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
          <tr
    v-for="(item, index) in items"
    :key="index"
    class="border-b border-gray-300"
  >
    <td class="px-2 py-1">{{ index + 1 }}</td>
    <td class="px-4 py-2 font-semibold">{{ item.description }}</td>
    <td class="px-4 py-2">{{ item.quantity }} PC</td>
    <td class="px-4 py-2">${{ item.price }}</td>
    <td class="px-4 py-2 text-green-700 font-semibold">${{ item.total }}</td>
  </tr>
         
        </tbody>
      </table>
    </div>

    <!-- fourth section -->

    <div class="flex justify-between lg:mx-10 md:mx-10 ml-2  mt-6 border-b-2  border-green-300 ">
      <div>
        <div>
          <h1 class="font-bold text-[#0ace7cd8] text-[17px]">Payment Info</h1>
          <p>evc0619538337/ <br>edhab 0629538337</p>
        </div>

        <div class=" ">
          <h1 class="font-bold text-[#0ace7cd8] text-[17px]">Served by</h1>
          <p>{{items[0]?.served}}</p>
        </div>
        <div>
          <img class="w-[200px]"
            src="../assets/Black and Blue Mobile Phone Repair Logo.png"
            alt=""
          />
        </div>
        

      </div>
      <div class="w-full lg:w-auto md:w-auto sm:auto mb-4  mr-0">
         <div class="mb-[16px]">
           <span class=" bg-teal-500 font-bold text-white text-[15px] py-2 ml-5  lg:pl-4 md:pl-4 pl-[5px] lg:pr-10 md:pr-10 pr-3">TOTAL AMOUNT</span>
           <span class="inline-block bg-teal-400 font-bold text-white py-[6px] pl-4 w-[70px] lg:w-[140px] md:w-[140px]">${{ totalPrice }}</span>
           
         </div> 
         <div class="mb-[16px]">
           <span class="bg-teal-500 font-bold text-white text-[15px] py-2 ml-5  lg:pl-4 md:pl-4 pl-[5px] lg:pr-[82px] md:pr-[82px] pr-[50px]">DISCOUNT</span>
           <span class="inline-block bg-teal-400 font-bold text-white py-[6px] pl-4 w-[70px] lg:w-[140px] md:w-[140px]">${{items[0]?.discount}}</span>
           
         </div> 
           
         <div class="mb-[16px]">
           <span class="bg-teal-500 font-bold text-white text-[15px] py-2 ml-5  lg:pl-4 md:pl-4 pl-[5px] lg:pr-[123px] md:pr-[123px] pr-[91px]">PAID</span>
           <span class="inline-block bg-teal-400 font-bold text-white py-[6px] pl-4 w-[70px] lg:w-[140px] md:w-[140px]">${{items[0]?.paid}}</span>

         </div> 
         <div>
           <span class="bg-teal-500 font-bold text-white text-[15px] py-2 ml-5  lg:pl-4 md:pl-4 pl-[5px] lg:pr-[90px] md:pr-[90px] pr-[57px]">BALANCE</span>
           <span class="inline-block bg-teal-400 font-bold text-white py-[6px] pl-4 w-[70px] lg:w-[140px] md:w-[140px]">${{items[0]?.balance}}</span>

         </div>

        </div>
    </div>
    <h1 class="font-bold text-green-700 mt-5 mb-20 ml-10">thank you {{ items[0]?.name }} for the purchase</h1>

    <button onclick="window.print()" class="bg-blue-500 text-white px-4 py-2 rounded">
  Print
</button>

  </div>
</template>

<script>
export default {
  name: "Result",
  data() {
    const today = new Date();
    return {
      data:{
      month: today.toLocaleString('default', { month: 'long' }),
      day: today.getDate(),
      year: today.getFullYear(),
      }
    };
  },
  props: {
    items: {
      type: Array,
      required: true,
    },
  },

  computed: {
    totalPrice() {
      return this.items.reduce((sum, item) => sum + item.total - item.discount, 0);
    },
  },
};
</script>

<style>
body{
  padding:0;
  margin:0;
}
</style>

<!-- <div class="flex flex-col gap-3 mx-5  ">
       <div class="flex bg-green-500 text-white font-bold py-3">
        <p class="flex-1 pl-3">item description</p>
        <p class="mr-5">Quantity</p>
        <p class="mr-5">price</p>
        <p class="mr-5">total</p>
       </div>
       <div class="flex font-bold py-3  ">
        <p class="flex-1 ">milk</p>
        <p class="mr-5">4 </p>
        <p class="mr-5">100</p>
        <p class="mr-5">400</p>

       </div> -->
