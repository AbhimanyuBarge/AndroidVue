<script setup>
import { Download, FileText } from '@lucide/vue'

const triggerPrint = () => {
  window.print()
}
</script>

<template>
  <div class="flex flex-col sm:flex-row items-center justify-center gap-4 mt-8 mb-16 no-print">
    <!-- Action Button -->
    <button 
      @click="triggerPrint"
      class="group relative inline-flex items-center gap-2.5 px-8 py-4 rounded-2xl bg-gradient-to-r from-blue-600 via-indigo-600 to-purple-600 text-white font-semibold text-base shadow-lg shadow-indigo-500/20 hover:shadow-indigo-500/40 hover:-translate-y-0.5 active:translate-y-0 transition-all cursor-pointer overflow-hidden">
      <!-- Glow effect -->
      <span class="absolute inset-0 w-full h-full bg-gradient-to-r from-white/0 via-white/20 to-white/0 -translate-x-full group-hover:animate-[shimmer_1.5s_infinite]"></span>
      
      <Download class="h-5 w-5 group-hover:scale-110 transition-transform" />
      <span>Download Resume as PDF</span>
    </button>

    <!-- Floating Action Button for easy access on desktop -->
    <button 
      @click="triggerPrint"
      class="fixed bottom-6 right-6 z-50 p-4 rounded-full bg-indigo-600 text-white shadow-xl shadow-indigo-600/30 hover:bg-indigo-500 hover:scale-110 active:scale-95 transition-all cursor-pointer md:flex items-center justify-center hidden border border-indigo-400/25"
      title="Download PDF">
      <FileText class="h-6 w-6" />
    </button>
  </div>
</template>

<style scoped>
@keyframes shimmer {
  100% {
    transform: translateX(100%);
  }
}
</style>
