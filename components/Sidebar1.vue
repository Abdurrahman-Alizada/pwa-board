<template>
    <div>
       <span v-for="(item, index) in lsubItems" :key="index" class="flex items-end">
          <div class="bg-gray-700 w-full py-2 px-1">
      <div class="flex items-center"> 
         <img alt="avatar" class="w-8 rounded-full " src="https://picsum.photos/seed/picsum/200" />
         <div class="ml-1">
            <p class="text-sm text-gray-100 font-semibold">{{item.name}}</p>
            <p class="text-xs text-gray-400">3 open, 4 closed</p>
         </div> 
      </div>
<!-- progress bar -->
          <div class="w-full mt-1 bg-gray-100 rounded-full h-1.5 dark:bg-gray-700">
            <div class="bg-green-300 h-1.5 rounded-full dark:bg-gray-300" style="width: 45%"></div>
          </div>
   </div>
        </span>         
    </div>

</template>

<script>
export default {
  data(){
      return{
          isOpen: false,
          lsubItems : this.subItems
      }
  },
  props: {
      subItems :{
          type : Array
      }
  },
    methods: {
    drawer() {
      this.isOpen = !this.isOpen;
    }
  },
}
</script>

<style>
</style>