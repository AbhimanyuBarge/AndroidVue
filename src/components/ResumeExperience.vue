<script setup>
import { ref } from 'vue'
import { Briefcase, Calendar, ChevronDown, ChevronUp } from '@lucide/vue'

defineProps({
  experience: {
    type: Array,
    required: true
  }
})

const expandedProjects = ref({})

const toggleProject = (index) => {
  expandedProjects.value[index] = !expandedProjects.value[index]
}
</script>

<template>
  <section class="rounded-3xl border border-slate-800/60 bg-slate-900/40 p-8 md:p-12 backdrop-blur-xl shadow-xl print-card">
    <h3 class="text-2xl font-bold tracking-tight text-white mb-8 flex items-center gap-3 print-title">
      <Briefcase class="h-6 w-6 text-blue-400 no-print" /> Experience
    </h3>

    <!-- Timeline Container -->
    <div class="relative border-l border-slate-800 ml-4 md:ml-6 pl-6 md:pl-10 space-y-12 print-card">
      <div v-for="(exp, expIdx) in experience" :key="expIdx" class="relative group">
        <!-- Timeline dot -->
        <span class="absolute -left-[31px] md:-left-[47px] top-1.5 flex h-4 w-4 md:h-6 md:w-6 items-center justify-center rounded-full bg-slate-900 border-2 border-blue-500 group-hover:border-purple-400 transition-colors shadow-[0_0_10px_rgba(59,130,246,0.3)] no-print">
          <span class="h-1.5 w-1.5 md:h-2 md:w-2 rounded-full bg-blue-500 group-hover:bg-purple-400 transition-colors"></span>
        </span>

        <!-- Experience Metadata -->
        <div class="flex flex-col md:flex-row md:items-center justify-between gap-2 mb-3">
          <div>
            <h4 class="text-xl font-bold text-white group-hover:text-blue-400 transition-colors print-sub-title">
              {{ exp.role }}
            </h4>
            <div class="text-slate-400 print-text-muted font-medium text-sm">
              {{ exp.company }} &middot; <span class="text-blue-400/90 print-sub-title">{{ exp.location }}</span>
            </div>
          </div>
          <div class="flex items-center gap-2 text-xs font-semibold text-slate-400 bg-slate-800/60 border border-slate-700/50 px-3 py-1 rounded-full w-fit group-hover:border-blue-500/30 transition-colors print-text-muted">
            <Calendar class="h-3.5 w-3.5 text-blue-400 no-print" />
            <span>{{ exp.period }}</span>
          </div>
        </div>

        <!-- Projects list under this experience -->
        <div class="space-y-6 mt-4">
          <div v-for="(project, projIdx) in exp.projects" :key="projIdx" 
               class="p-5 rounded-2xl bg-slate-800/30 border border-slate-800 hover:border-slate-700/50 transition-all shadow-inner print-card">
            
            <!-- Project Header -->
            <div class="flex items-center justify-between cursor-pointer no-print" @click="toggleProject(expIdx + '-' + projIdx)">
              <h5 class="text-base font-semibold text-blue-400 flex items-center gap-2">
                Project: {{ project.name }}
                <span v-if="project.client" class="text-xs font-normal text-slate-400">({{ project.client }})</span>
              </h5>
              <button class="text-slate-400 hover:text-white transition-colors" aria-label="Toggle project details">
                <ChevronUp v-if="expandedProjects[expIdx + '-' + projIdx] !== false" class="h-4 w-4" />
                <ChevronDown v-else class="h-4 w-4" />
              </button>
            </div>

            <!-- Print-only Project Header -->
            <h5 class="hidden print:block text-base font-semibold text-blue-800 print-sub-title print-compact-margin">
              Project: {{ project.name }} <span v-if="project.client" class="text-xs font-normal text-slate-600">({{ project.client }})</span>
            </h5>

            <!-- Project Body (Collapsible on Web, Always open on Print) -->
            <div v-show="expandedProjects[expIdx + '-' + projIdx] !== false" class="mt-3 space-y-3 print:block">
              <p class="text-sm text-slate-300 print-text-muted leading-relaxed">
                {{ project.description }}
              </p>
              
              <!-- Roles and Responsibilities -->
              <div>
                <div class="text-xs font-semibold text-slate-400 uppercase tracking-wider mb-2 print-sub-title">Roles & Responsibilities</div>
                <ul class="list-disc pl-5 space-y-1.5 text-sm text-slate-300 print-text-muted">
                  <li v-for="(role, roleIdx) in project.roles" :key="roleIdx">
                    {{ role }}
                  </li>
                </ul>
              </div>

              <!-- Project Stack Tag Badges (no-print optional, but let's keep clean simple print version if relevant) -->
              <div v-if="project.tech" class="flex flex-wrap gap-1.5 pt-2">
                <span v-for="(t, tIdx) in project.tech" :key="tIdx" 
                      class="text-xs px-2 py-0.5 rounded bg-slate-900 border border-slate-700 text-slate-300 print-skills-badge">
                  {{ t }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
