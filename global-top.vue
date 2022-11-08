<script setup lang="ts">
import { computed } from 'vue'
import { useNow } from '@vueuse/core'
import { useTimer } from './setup/utils'

const now  = useNow()
const { timer, passed } = useTimer()

// const END_THIS_NOW = 5

  console.log('now', now)
  console.log('timer.value', timer.value)
  console.log('passed.value', passed.value)

const options = { weekday: 'short', year: 'numeric', month: 'long', day: 'numeric' };
const date = computed(() => now?.value.toLocaleDateString($slidev.configs.dateFormat, options))

const compute =  computed(() => passed.value > $slidev.configs.presentationEnd)

  const LayoutWithoutDate = [
      'image-right',
      'iframe-right',
      'image-left',
      'iframe-left',
  ]
  
const LayoutWithoutFooter = [
    'iframe',
    ...LayoutWithoutDate
]


const LayoutWithoutName = [
    'image-left',
    'iframe-left',
]

const LayoutWithoutPageNumber = [
    'image-right',
    'iframe-right',
]



function logTimers (){
  console.log('timer.value', timer.value)
  console.log('passed.value', passed.value)
  console.log('compute.value', compute.value)
}

</script>



<template>
  <header
    v-if="!LayoutWithoutName.includes($slidev.nav.currentLayout)"
    class="absolute top-0 p-2 text-sm w-full h-6"
  >

  <div
  v-if="compute"
  class="top-0 left-0 opacity-95 absolute h-132 w-245 w-full bg-main border-light-warning dark:border-dark-warning border-3 justify-center flex items-center text-light-warning dark:text-dark-warning font-bold text-4xl"
  >{{$slidev.configs.presentationEndMessage}} {{ timer }}</div>



  <div 
    class="absolute top-0"
    @click="logTimers()"
      v-if="!LayoutWithoutName.includes($slidev.nav.currentLayout)">
      

      
      </div>

      <div 
    class="absolute top-0 left-100"
    @click="logTimers()"
      v-if="!LayoutWithoutName.includes($slidev.nav.currentLayout)">
      

      
      </div>
    </header>
</template>

<style scoped>
header {
  @apply font-mono  text-brand-darker dark:text-brand-light bg-brand-light dark:bg-light-text;
}

</style>