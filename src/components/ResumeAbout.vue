<script setup>
import { Briefcase, User, Award, Code2 } from '@lucide/vue'

defineProps({
  summary: {
    type: String,
    required: true
  }
})
</script>

<template>
  <section class="rounded-3xl border border-slate-800/60 bg-slate-900/40 p-8 md:p-12 backdrop-blur-xl shadow-xl print-card">
    <h3 class="text-2xl font-bold tracking-tight text-white mb-6 flex items-center gap-3 print-title">
      <User class="h-6 w-6 text-blue-400 no-print" /> About Me
    </h3>
    
    <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 items-start print-grid">
      <!-- Summary Text -->
      <div class="lg:col-span-2 text-slate-300 print-text-muted leading-relaxed text-base">
        <p class="mb-4">
          {{ summary }}
        </p>
        <p class="no-print">
          Passionate about building scalable backend architectures, cloud-native services, and robust APIs. Proven track record of successfully leading data migration and ETL jobs, orchestrating container deployments, and writing high-quality tested code that drives business value.
        </p>
      </div>

      <!-- Quick Highlights Grid -->
      <div class="grid grid-cols-2 gap-4 lg:col-span-1 print-grid">
        <div class="p-4 rounded-2xl bg-slate-800/50 border border-slate-700/50 flex flex-col items-center justify-center text-center group hover:border-blue-500/50 transition-all print-card print-compact-margin">
          <Award class="h-6 w-6 text-blue-400 mb-2 no-print group-hover:scale-110 transition-transform" />
          <span class="text-2xl font-bold text-white print-sub-title">10+ Years</span>
          <span class="text-xs text-slate-400 print-text-muted mt-1">Professional Experience</span>
        </div>
        <div class="p-4 rounded-2xl bg-slate-800/50 border border-slate-700/50 flex flex-col items-center justify-center text-center group hover:border-blue-500/50 transition-all print-card print-compact-margin">
          <Briefcase class="h-6 w-6 text-blue-400 mb-2 no-print group-hover:scale-110 transition-transform" />
          <span class="text-2xl font-bold text-white print-sub-title">9+ Years</span>
          <span class="text-xs text-slate-400 print-text-muted mt-1">Golang & Backend Focus</span>
        </div>
        <div class="p-4 rounded-2xl bg-slate-800/50 border border-slate-700/50 flex flex-col items-center justify-center text-center group hover:border-blue-500/50 transition-all print-card print-compact-margin col-span-2 print-col-sidebar">
          <Code2 class="h-6 w-6 text-blue-400 mb-2 no-print group-hover:scale-110 transition-transform" />
          <span class="text-lg font-semibold text-white print-sub-title">GO lang Expert</span>
          <span class="text-xs text-slate-400 print-text-muted mt-1">REST APIs, Microservices</span>
        </div>
      </div>
    </div>
  </section>
</template>
