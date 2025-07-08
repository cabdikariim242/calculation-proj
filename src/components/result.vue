<template>
  <div class="mt-0">

    <!-- nav bar section -->
    <div class="flex  justify-between items-center text-black ">
      <div class="bg-gray-700 rounded">
        <img class="w-[200px] bg-gray-700" src="../assets/Black and Blue Mobile Phone Repair Logo.png" alt="LOGO">

       </div>
       <div class="mr-20">
        <h1 class="font-bold text-[#0ace7cd8] text-[30px]">SALES</h1>
        <P class="font-bold text-[12px]">JUN 04, 2025</P>

      </div>
    </div>
    <div>
      <!-- hero section -->

      <div class="flex  justify-between items-center text-black ">
        <div class="ml-10">
          <h1 class="font-bold text-[#0ace7cd8] text-[20px]">AWOOWE  ELECTRONICS</h1>
          <P>Soobe, Abdishideeye, somalia</P>
          <p>0619538337/0612498658</p>
          <p>awoowe@gmail.com</p>
        </div>
        <div class="mr-20">
          <h1 class="font-bold text-[#0ace7cd8] text-[17px]">BILL TO</h1>
          <p class="font-bold text-[#0ace7cd8] text-[14px]">awoowe</p>
          <p class="font-[400]">619538337</p>
        </div>
            </div>

      </div>

      <!-- third section -->
      <div class="mt-10">
         <table class="min-w-full border border-gray-300">
      <thead>
        <tr class="bg-teal-700 text-white text-left">
          <th class="px-4 py-2 border-r border-white">#</th>
          <th class="px-4 py-2 border-r border-white">Item Description</th>
          <th class="px-4 py-2 border-r border-white">Quantity</th>
          <th class="px-4 py-2">Price</th>
        </tr>
      </thead>
      <tbody class="bg-white text-sm">
        <tr class="border-b border-gray-300">
          <td class="px-4 py-2">1</td>
          <td class="px-4 py-2 font-semibold">a04e aa (LCD)</td>
          <td class="px-4 py-2">1 PC</td>
          <td class="px-4 py-2 text-green-700 font-semibold">$7</td>
        </tr>
      </tbody>
    </table>
      </div>

      <!-- fourth section -->

      <div>
        <div>
          
        </div>
        <div></div>
      </div>
     


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