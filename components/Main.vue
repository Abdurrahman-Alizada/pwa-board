<template>
<div class="relative flex overflow-auto">
 <!-- left side -->
  <div class="h-screen overflow-y-scroll top-0 sticky">
    <!-- Note: add overflow-y-scroll if sidebar content is longer than page -->
   <Home />
  </div>
  <!-- right side -->
  <div class="flex-grow w-full overflow-auto ml-16 p-4 bg-gray-100">   
    <Content />
    <Content />
    <Content />
    <Content />
    <Content />
    <Content />
    <Content />
  </div>
    <div class="flex top-1/2 right-0 fixed justify-center items-center">
      <button class="inline-flex items-center justify-center border border-transparent text-sm font-medium rounded-lg w-16 h-16 text-white bg-green-500 hover:bg-green-700 transition-colors">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
      </svg>
      </button>
    </div>

</div>
</template>

<script>
import Home from './Home.vue'
import Content from './content.vue'
export default {

components :{
    Home, Content
}
}
</script>

<style>

</style>