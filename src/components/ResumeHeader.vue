<script setup>
import { Mail, Phone, MapPin } from '@lucide/vue'

defineProps({
  name: {
    type: String,
    required: true
  },
  title: {
    type: String,
    required: true
  },
  contact: {
    type: Object,
    required: true
  }
})
</script>

<template>
  <header class="relative overflow-hidden rounded-3xl border border-slate-800/60 bg-slate-900/40 p-8 md:p-12 backdrop-blur-xl shadow-xl print-card">
    <!-- Background glow -->
    <div class="absolute -right-20 -top-20 h-64 w-64 rounded-full bg-blue-500/10 blur-3xl no-print"></div>
    <div class="absolute -left-20 -bottom-20 h-64 w-64 rounded-full bg-indigo-500/10 blur-3xl no-print"></div>

    <div class="relative z-10 flex flex-col md:flex-row md:items-center md:justify-between gap-8">
      <div>
        <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-semibold bg-blue-500/10 text-blue-400 border border-blue-500/20 mb-4 animate-pulse-subtle no-print">
          <span class="h-2 w-2 rounded-full bg-blue-400"></span> Available for New Opportunities
        </span>
        <h1 class="text-4xl md:text-6xl font-bold tracking-tight bg-gradient-to-r from-white via-slate-100 to-blue-400 bg-clip-text text-transparent print-title !m-0 !p-0">
          {{ name }}
        </h1>
        <h2 class="text-xl md:text-2xl font-medium text-blue-400 mt-2 print-sub-title">
          {{ title }}
        </h2>
      </div>

      <!-- Contact Info -->
      <div class="flex flex-col gap-3 text-slate-300 print-text-muted text-sm md:text-right md:items-end">
        <a :href="'tel:' + contact.phone" class="flex items-center gap-2 hover:text-blue-400 transition-colors group">
          <span>{{ contact.phone }}</span>
          <Phone class="h-4 w-4 text-blue-400 group-hover:scale-110 transition-transform" />
        </a>
        <a :href="'mailto:' + contact.email" class="flex items-center gap-2 hover:text-blue-400 transition-colors group">
          <span>{{ contact.email }}</span>
          <Mail class="h-4 w-4 text-blue-400 group-hover:scale-110 transition-transform" />
        </a>
        <div class="flex items-center gap-2">
          <span>{{ contact.location }}</span>
          <MapPin class="h-4 w-4 text-blue-400" />
        </div>
        
        <!-- Social Links -->
        <div class="flex gap-3 mt-2 no-print">
          <a :href="contact.linkedin" target="_blank" rel="noopener noreferrer" 
             class="p-2.5 rounded-xl bg-slate-800/80 border border-slate-700 hover:border-blue-500 hover:bg-slate-800 hover:text-blue-400 transition-all shadow-md hover:shadow-lg hover:shadow-blue-500/10 flex items-center justify-center"
             aria-label="LinkedIn Profile">
            <svg class="h-4 w-4 fill-current" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
              <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
            </svg>
          </a>
          <a :href="contact.github" target="_blank" rel="noopener noreferrer" 
             class="p-2.5 rounded-xl bg-slate-800/80 border border-slate-700 hover:border-blue-500 hover:bg-slate-800 hover:text-blue-400 transition-all shadow-md hover:shadow-lg hover:shadow-blue-500/10 flex items-center justify-center"
             aria-label="GitHub Profile">
            <svg class="h-4 w-4 fill-current" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
              <path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/>
            </svg>
          </a>
        </div>
      </div>
    </div>
  </header>
</template>

