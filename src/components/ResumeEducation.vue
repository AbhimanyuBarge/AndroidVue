<script setup>
import { GraduationCap, Award, Calendar, BookOpen } from '@lucide/vue'

defineProps({
  education: {
    type: Array,
    required: true
  },
  courses: {
    type: Array,
    required: true
  }
})
</script>

<template>
  <section class="grid grid-cols-1 lg:grid-cols-2 gap-8 print-grid">
    <!-- Education Column -->
    <div class="rounded-3xl border border-slate-800/60 bg-slate-900/40 p-8 md:p-12 backdrop-blur-xl shadow-xl print-card">
      <h3 class="text-2xl font-bold tracking-tight text-white mb-8 flex items-center gap-3 print-title">
        <GraduationCap class="h-6 w-6 text-blue-400 no-print" /> Education
      </h3>

      <div class="space-y-8 print-card">
        <div v-for="(edu, idx) in education" :key="idx" class="relative pl-6 border-l-2 border-slate-800 hover:border-blue-500/50 transition-colors group">
          <!-- Small dot on line -->
          <span class="absolute -left-1.5 top-1.5 h-3.5 w-3.5 rounded-full bg-slate-900 border-2 border-slate-700 group-hover:border-blue-500 transition-colors"></span>
          
          <h4 class="text-base font-bold text-white group-hover:text-blue-400 transition-colors print-sub-title">
            {{ edu.degree }}
          </h4>
          <p class="text-sm font-semibold text-slate-400 mt-1 print-text-muted">
            {{ edu.institution }}
          </p>
          <div class="flex items-center gap-1.5 text-xs text-slate-500 print-text-muted mt-2">
            <Calendar class="h-3.5 w-3.5 text-blue-400/80 no-print" />
            <span>{{ edu.period }}</span>
          </div>
          <p v-if="edu.description" class="text-sm text-slate-300 print-text-muted mt-3 leading-relaxed">
            {{ edu.description }}
          </p>
        </div>
      </div>
    </div>

    <!-- Courses/Certificates Column -->
    <div class="rounded-3xl border border-slate-800/60 bg-slate-900/40 p-8 md:p-12 backdrop-blur-xl shadow-xl print-card">
      <h3 class="text-2xl font-bold tracking-tight text-white mb-8 flex items-center gap-3 print-title">
        <Award class="h-6 w-6 text-blue-400 no-print" /> Certifications & Courses
      </h3>

      <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 print-grid print-compact-margin">
        <div v-for="(course, idx) in courses" :key="idx" 
             class="p-4 rounded-2xl bg-slate-800/30 border border-slate-800 hover:border-blue-500/30 hover:bg-slate-800/50 transition-all flex items-start gap-3 print-card print-compact-margin">
          <div class="p-2 rounded-xl bg-slate-800/80 border border-slate-700 text-blue-400 mt-0.5 no-print">
            <BookOpen class="h-4 w-4" />
          </div>
          <div>
            <h4 class="text-sm font-bold text-white print-sub-title leading-tight">
              {{ course.name }}
            </h4>
            <p class="text-xs text-slate-400 print-text-muted mt-1">
              {{ course.provider }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
