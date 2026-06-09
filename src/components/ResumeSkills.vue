<script setup>
import { ref, computed } from 'vue'
import { Code2, Server, Database, AppWindow, Cpu } from '@lucide/vue'

const props = defineProps({
  skills: {
    type: Array,
    required: true
  }
})

const activeFilter = ref('All')
const categories = ['All', 'Languages', 'DevOps & Cloud', 'Database', 'Tools']

const filteredSkills = computed(() => {
  if (activeFilter.value === 'All') {
    return props.skills
  }
  return props.skills.filter(s => s.category === activeFilter.value)
})

const getCategoryIcon = (cat) => {
  switch (cat) {
    case 'Languages': return Code2
    case 'DevOps & Cloud': return Cpu
    case 'Database': return Database
    default: return AppWindow
  }
}
</script>

<template>
  <section class="rounded-3xl border border-slate-800/60 bg-slate-900/40 p-8 md:p-12 backdrop-blur-xl shadow-xl print-card">
    <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 mb-8">
      <h3 class="text-2xl font-bold tracking-tight text-white flex items-center gap-3 print-title">
        <Code2 class="h-6 w-6 text-blue-400 no-print" /> Technical Skills
      </h3>
      
      <!-- Category Filter Toggles -->
      <div class="flex flex-wrap gap-2 no-print">
        <button 
          v-for="cat in categories" 
          :key="cat"
          @click="activeFilter = cat"
          :class="[
            'px-4 py-1.5 rounded-full text-xs font-semibold border transition-all cursor-pointer',
            activeFilter === cat 
              ? 'bg-blue-500 border-blue-500 text-white shadow-md shadow-blue-500/20' 
              : 'bg-slate-800/60 border-slate-700 text-slate-300 hover:border-slate-600'
          ]">
          {{ cat }}
        </button>
      </div>
    </div>

    <!-- Skills Grid -->
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 print-grid print-compact-margin">
      <div v-for="(skill, idx) in filteredSkills" :key="idx" 
           class="p-5 rounded-2xl bg-slate-800/30 border border-slate-800 hover:border-blue-500/30 hover:bg-slate-800/50 transition-all group print-card print-compact-margin">
        
        <div class="flex items-center justify-between mb-3">
          <div class="flex items-center gap-3">
            <div class="p-2.5 rounded-xl bg-slate-800/80 border border-slate-700 text-blue-400 group-hover:text-purple-400 group-hover:border-purple-500/30 transition-colors no-print">
              <component :is="getCategoryIcon(skill.category)" class="h-4 w-4" />
            </div>
            <div>
              <h4 class="text-base font-bold text-white group-hover:text-blue-400 transition-colors print-sub-title">{{ skill.name }}</h4>
              <span class="text-[10px] text-slate-400 uppercase tracking-wider print-text-muted">{{ skill.category }}</span>
            </div>
          </div>
          <span class="text-sm font-semibold text-slate-300 print-text-muted">{{ skill.level }}%</span>
        </div>

        <!-- Progress bar container -->
        <div class="h-2 w-full bg-slate-800 rounded-full overflow-hidden no-print">
          <div 
            class="h-full bg-gradient-to-r from-blue-500 to-indigo-500 rounded-full group-hover:from-purple-500 group-hover:to-pink-500 transition-all duration-500" 
            :style="{ width: skill.level + '%' }">
          </div>
        </div>

        <!-- Print-only text for level instead of progress bars -->
        <div class="hidden print:block text-xs text-slate-500 print-text-muted mt-1">
          Expertise Level: {{ skill.level }}% (Advanced/Expert)
        </div>
      </div>
    </div>

    <!-- Print-only Skills Compact Badge View -->
    <div class="hidden print:block mt-6">
      <div class="text-xs font-semibold text-slate-600 uppercase tracking-wider mb-2 print-sub-title">Skills Overview</div>
      <div class="flex flex-wrap gap-2">
        <span v-for="(skill, idx) in skills" :key="'badge-'+idx" class="print-skills-badge">
          {{ skill.name }} ({{ skill.level }}%)
        </span>
      </div>
    </div>
  </section>
</template>
