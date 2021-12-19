<template>
        
  <div class="flex fixed w-full items-center justify-between h-16 bg-white text-gray-700 border-b border-gray-200 z-10">
<!-- navbar -->
       <div   class="flex items-center justify-center">
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
      <transition
      enter-class="opacity-0"
      enter-active-class="ease-out transition-medium"
      enter-to-class="opacity-100"
      leave-class="opacity-100"
      leave-active-class="ease-out transition-medium"
      leave-to-class="opacity-0"
    >
      <div
        @keydown.esc="isOpen = false"
        v-show="isOpen"
        class="z-10 fixed inset-0 transition-opacity"
      >
        <div
          @click="isOpen = false"
          class="absolute inset-0 opacity-50"
          tabindex="0"
        ></div>
      </div>
    </transition>
    
    <aside class="transform top-0 left-0 w-16 mt-16 bg-gray-600 fixed h-full overflow-auto ease-in-out transition-all duration-300 z-30">
      <span v-for="(item, index) in items" :key="index" @click="selectedItem(index)" class="flex items-center justify-center p-4 text-white hover:bg-gray-700 hover:text-green-400 ">
        <span class="mr-2">
          <div v-html="item.svg "></div>
        </span>
      </span>        
    </aside> 
<!-- second sidebar -->
    <aside class="transform mt-16 ml-16 top-0 left-0 w-48 bg-gray-700 border-r border-gray-300 fixed h-full overflow-auto ease-in-out transition-all duration-700 z-0"  
      :class="isOpen ? 'translate-x-0' : '-translate-x-full'" 
     >
     <Sidebar :key="componentKey" :subItems="items[selectedIndex].subItems" />
    </aside>
   <!-- end second sidebar -->
   <!-- dropdown -->
   
   <Dropdown v-if="dropdown" />
  </div>


</template>

<script>
import Sidebar from './Sidebar1'
// import Dropdown from './Dropdown.vue'
import Content from './content.vue'
import svg1 from '../assets/svgs/1.vue'
import Dropdown from './Dropdown.vue';

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
      console.log(this.isOpen)
    },
    selectedItem(index){
      this.selectedIndex = index;
      this.isOpen = true;
    },
    showdropdown(){
      this.dropdown = !this.dropdown
    },
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
         this.componentKey += 1;
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
    Content,
    Dropdown
}
};
</script>

<style scoped>

</style>
