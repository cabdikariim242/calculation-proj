<!-- <template>
  this is about page
  <h1 class="text-3xl font-bold underline">About</h1>
  <p class="mt-4">This is the about page of our application.</p>
  <p class="mt-2">Here you can find information about the app and its features.</p>
  <p class="mt-2">Feel        free to explore and learn more about what we offer!</p>
</template> -->

<template>
<div class="flex justify-center items-center h-screen ">
    <input type="date" v-model="date" class="p-2 border rounded py-10 px-20" />
  
    
  </div>
</template>

<script >
export default {
  data() {
    return {
      date: null
    }
  },
}

</script>