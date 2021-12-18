<template>
<!-- navbar -->
  <nav class="flex fixed w-full items-center justify-between h-16 bg-white text-gray-700 border-b border-gray-200 z-10">
       <div class="flex items-center justify-center">
        <button class="h-16 flex items-center justify-center w-16 border-r border-gray-400" aria-label="Open Menu" @click="drawer">

        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"   :d="isOpen ? 'M15 19l-7-7 7-7' : 'M9 5l7 7-7 7'"  />
        </svg>
        </button>
         <div class="ml-5 flex text-green-700 font-bold text-xl items-center justify-center">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          <span class="ml-1">morpheus</span>
         </div>
       </div>
    <button  class="h-16 flex items-center justify-center w-16 border-r border-gray-400" aria-label="Open Menu" @click="showdropdown">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
      </svg>
    </button>  
<!-- end navbar -->
<!-- sidebar -->
    <aside class="transform top-0 left-0 w-16 mt-16 bg-gray-600 fixed h-full overflow-auto ease-in-out transition-all duration-300 z-30">
      <span v-for="(item, index) in items" :key="index" @click="selectedItem(index)" class="flex items-center justify-center p-4 text-white hover:bg-gray-700 hover:text-green-400 ">
        <span class="mr-2">
          <div v-html="item.svg "></div>
        </span>
      </span>        
    </aside> 
<!-- second sidebar -->
    <aside class="transform mt-16 ml-16 top-0 left-0 w-36 bg-gray-700 border-r border-gray-300 fixed h-full overflow-auto ease-in-out transition-all duration-300 z-0"  
     :class="isOpen ? 'translate-x-0' : '-translate-x-full'" 
     >
     <Sidebar :key="componentKey" :subItems="items[selectedIndex].subItems" />
    </aside>
<!-- end second sidebar -->
<!-- dropdown -->
      <div v-if="dropdown" class="right-0 top-0 absolute mt-16 w-56 rounded-md shadow-lg bg-gray-100 ring-1 ring-black ring-opacity-5 focus:outline-none">
        <div class="py-1" >
    

          <span class="flex items-center justify-start pl-4 ">
            <span class="flex items-center justify-center">
            
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
            </svg>
            <a href="#" class="text-gray-700 block px-4 py-2 text-sm ">Search</a>
            </span>
          <span></span>
          </span>

          <span class="flex items-center justify-between px-4 hover:bg-gray-300">
            <span class="flex items-center justify-center">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
            </svg>
            <a class="text-gray-700 block px-4 py-2 text-sm">Notification</a>
            </span>
          <span class="text-xs font-semibold inline-block py-1 px-2 rounded text-white bg-green-600 uppercase last:mr-0 mr-1">
            10
          </span>


          </span>


          <span class="flex items-center justify-start pl-4 hover:bg-gray-300">
            <span class="flex items-center justify-center">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 10h.01M12 10h.01M16 10h.01M9 16H5a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v8a2 2 0 01-2 2h-5l-5 5v-5z" />
            </svg>
            <a href="#" class="text-gray-700 block px-4 py-2 text-sm">Message</a>
            </span>
            <span>
            </span>           
          </span>
          
          <span class="flex items-center justify-start pl-4 hover:bg-gray-300">
            <span class="flex items-center justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
            </svg>
            <a href="#" class="text-gray-700 block px-4 py-2 text-sm">Settings</a>
            </span>
            <span>
              
            </span>           
          </span>

          <span class="flex items-center justify-start pl-4 hover:bg-gray-300">
            <span class="flex items-center justify-center">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
            </svg>
            <a href="#" class="text-gray-700 block px-4 py-2 text-sm">Profile</a>
            </span>
            <span>
              
            </span>           
          </span>
          
        </div>
      </div>

  </nav>


</template>

<script>
import Sidebar from './Sidebar1'
import Content from './content.vue'
import svg1 from '../assets/svgs/1.vue'

export default {
  data() {
    return {
      items : [
        {
          name : 'Home 1',
          svg : `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 19a2 2 0 01-2-2V7a2 2 0 012-2h4l2 2h4a2 2 0 012 2v1M5 19h14a2 2 0 002-2v-5a2 2 0 00-2-2H9a2 2 0 00-2 2v5a2 2 0 01-2 2z" />
                </svg>`, 
          subItems : [
            {name : 'Subitem 1'},{name : 'Subitem 2'},{name : 'Subitem 3'}
            ]
        },
        {
          name : 'Home 2',
          svg : `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                </svg>`, 
         subItems : [
            {name : '2 Subitem 1'},{name : '2 Subitem 2'},{name : '2 Subitem 3'}
          ]
        },
        {
          name : 'Home 4',
          svg : `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
                </svg>`,
          subItems : [
            {name : '4 Subitem 1'},{name : '4 Subitem 2'},{name : '4 Subitem 3',}
          ]
        },
        {
          name : 'Home 4',
          svg : `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 8v8m-4-5v5m-4-2v2m-2 4h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
                </svg>`,
          subItems : [
            {name : '3 Subitem 1'},{name : '3 Subitem 2'},{name : '3 Subitem 3',}
          ]
        },
        ],
         componentKey: 0,
      isOpen: false,
      selectedIndex : 0,
      dropdown : false
  };
  },
  methods: {
    drawer() {
      this.isOpen = !this.isOpen;
    },
    selectedItem(index){
      this.selectedIndex = index;
      console.log('in methods', index)
    },
    showdropdown(){
      this.dropdown = !this.dropdown
    }
  },
  watch: {
    isOpen: {
      immediate: true,
      handler(isOpen) {
        if (process.client) {
          if (isOpen) document.body.style.setProperty("overflow", "hidden");
          else document.body.style.removeProperty("overflow");
        }
      }
    },

        selectedIndex: {
      immediate: true,
      handler(index) {
        if (process.client) {
         this.selectedIndex = index
         console.log('in watch', index)
         this.componentKey += 1;
         // if (isOpen) document.body.style.setProperty("overflow", "hidden");
          // else document.body.style.removeProperty("overflow");
        }
      }
    }
  },
  mounted() {
    document.addEventListener("keydown", e => {
      if (e.keyCode == 27 && this.isOpen) this.isOpen = false;
    });
  },
  computed: {
  },
  components:{
    Sidebar, svg1,
    Content
}
};
</script>

<style scoped>

</style>
