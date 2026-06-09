<script setup>
import { ref, onMounted } from 'vue'
import ResumeHeader from './components/ResumeHeader.vue'
import ResumeAbout from './components/ResumeAbout.vue'
import ResumeExperience from './components/ResumeExperience.vue'
import ResumeSkills from './components/ResumeSkills.vue'
import ResumeEducation from './components/ResumeEducation.vue'
import DownloadButton from './components/DownloadButton.vue'
import { User, Briefcase, Code2, GraduationCap, ArrowUp } from '@lucide/vue'

const resumeData = {
  name: "Abhimanyu Barge",
  title: "Manager",
  contact: {
    phone: "+91 9657722210",
    email: "abhimanyubarge81@gmail.com",
    location: "Baramati, Pune, India",
    linkedin: "https://linkedin.com/in/abhimanyu-barge",
    github: "https://github.com/abhimanyubarge"
  },
  summary: "Software developer with over 10 years of experience, including 9 years as a backend developer specializing in Golang. Expert in building REST APIs, microservices, and ETL jobs. Skilled in Golang, Vue js, AWS, Kubernetes and Docker.",
  experience: [
    {
      role: "Manager",
      company: "Capgemini",
      location: "Pune, India",
      period: "March 2025 - Present",
      projects: [
        {
          name: "Lighthouse",
          client: "Charter Communication",
          description: "This tool generates alarms and automatically creates orders.",
          roles: [
            "Designed and implemented ETL pipelines using GoLang.",
            "Deployed solutions on AWS.",
            "Monitored data flows and system performance.",
            "Generated bulk reports for analysis."
          ],
          tech: ["Golang", "AWS", "Kafka", "Elasticsearch", "ETL", "Monitoring", "Reporting", "Kafka", "Elasticsearch"]
        }
      ]
    },
    {
      role: "Senior Consultant",
      company: "Capgemini",
      location: "Pune, India",
      period: "April 2024 - March 2025",
      projects: [
        {
          name: "Scope Migration",
          client: "Charter Communication",
          description: "Comprehensive migration of ETL jobs, services, and API servers from Cloudarea to AWS, leveraging AWS's powerful tools and services.",
          roles: [
            "Dockerization and creating deployment pipeline of REST API, ETL job.",
            "Deploying and managing containerized applications using Kubernetes on AWS.",
            "Using AWS Airflow service to schedule GO ETL jobs.",
            "Extracting data from various sources such as databases, APIs, and flat files.",
            "Identifying and resolving issues in the ETL processes."
          ],
          tech: ["Golang", "AWS", "Kubernetes", "Docker", "AWS Airflow", "ETL", "CI/CD"]
        }
      ]
    },
    {
      role: "Technical Lead",
      company: "Capgemini",
      location: "Pune, India",
      period: "June 2021 - April 2024",
      projects: [
        {
          name: "XOT",
          client: "Mercedes-Benz",
          description: "Transfer sensor data to the cloud, store it in MongoDB, and use the data to predict car servicing time and cost.",
          roles: [
            "Responsible for API design and development of RESTful APIs using Go.",
            "Built extensive test coverage reports for all new features using go test.",
            "Worked within an agile team and helped prioritize and scope feature requests.",
            "Designing and modeling MongoDB schemas to store data efficiently.",
            "Validating data before storing it in MongoDB to maintain data integrity.",
            "Writing unit tests for database interactions to ensure reliability."
          ],
          tech: ["Golang", "MongoDB", "RESTful API", "Unit Testing", "Agile", "API Design"]
        }
      ]
    },
    {
      role: "Senior Project Associate",
      company: "MKCL",
      location: "Pune, India",
      period: "October 2016 - June 2021",
      projects: [
        {
          name: "MP Vanamitra",
          client: "Ministry of Tribal Affairs",
          description: "Vanmitra has been developed with the objective of effective implementation of the Scheduled Tribes forest rights. Developed using VueJS, GoLang and MongoDB.",
          roles: [
            "Responsible for API design and development of RESTful APIs using Go.",
            "Built extensive test coverage reports for all new features using go test.",
            "Creating dynamic and responsive user interfaces using Vue.js components.",
            "Working closely with designers, backend developers, and other stakeholders."
          ],
          tech: ["Golang", "VueJS", "MongoDB", "REST API", "Frontend Integration"]
        },
        {
          name: "Labharthi",
          client: "MKCL",
          description: "Portal to search citizen benefit schemes. Prepared after studying citizens' 104 attributes and state resolutions.",
          roles: [
            "Responsible for API design and development of RESTful APIs using Go.",
            "Built extensive test coverage reports for all new features using go test.",
            "Creating dynamic and responsive user interfaces using Vue.js components.",
            "Working closely with stakeholders to deliver high-quality products."
          ],
          tech: ["Golang", "VueJS", "MongoDB", "REST API", "Database Design", "User Interface"]
        }
      ]
    }
  ],
  skills: [
    { name: "Golang", category: "Languages", level: 95 },
    { name: "JavaScript", category: "Languages", level: 85 },
    { name: "Vue js", category: "Languages", level: 85 },
    { name: "Java", category: "Languages", level: 70 },
    { name: "AWS", category: "DevOps & Cloud", level: 80 },
    { name: "Kubernetes", category: "DevOps & Cloud", level: 85 },
    { name: "Docker", category: "DevOps & Cloud", level: 90 },
    { name: "Kafka", category: "DevOps & Cloud", level: 85 },
    { name: "MongoDB", category: "Database", level: 85 },
    { name: "MySQL", category: "Database", level: 80 },
    { name: "PostgreSQL", category: "Database", level: 80 },
    { name: "Elasticsearch", category: "Database", level: 80 },
    { name: "Trino", category: "Database", level: 75 },
    { name: "VS Code", category: "Tools", level: 90 }
  ],
  education: [
    {
      degree: "PG Diploma - C-DAC",
      institution: "IACSD, Pune",
      period: "January 2016 - September 2016",
      description: "A Diploma in Advanced Software Development Methodologies (DASDM) is a specialized program providing in-depth training in software development."
    },
    {
      degree: "Computer Engineering | B.E",
      institution: "DKCOE, Baramati",
      period: "June 2011 - November 2015",
      description: ""
    },
    {
      degree: "Diploma in Computer Engineering",
      institution: "SVPM College Of Engineering, Baramati",
      period: "May 2008 - May 2011",
      description: ""
    }
  ],
  courses: [
    { name: "Go: The Complete Developer's Guide", provider: "Udemy" },
    { name: "Vue - The Complete Guide (Router, Vuex)", provider: "Udemy" },
    { name: "MongoDB - The Complete Developer's Guide", provider: "Udemy" },
    { name: "The Complete Node.js Developer Course", provider: "Udemy" }
  ]
}

const showScrollTop = ref(false)

const handleScroll = () => {
  showScrollTop.value = window.scrollY > 400
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const triggerPrint = () => {
  window.print()
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})
</script>

<template>
  <!-- Web Layout (Only visible on screen, hidden on print) -->
  <div class="min-h-screen bg-[#0b0f19] text-[#f3f4f6] relative selection:bg-blue-500/30 no-print">
    <!-- Navbar / Header Menu -->
    <nav class="sticky top-0 z-40 bg-[#0b0f19]/80 backdrop-blur-md border-b border-slate-800/80 px-6 py-4 shadow-md">
      <div class="max-w-6xl mx-auto flex items-center justify-between">
        <div class="flex items-center gap-2">
          <div class="h-9 w-9 rounded-xl bg-gradient-to-tr from-blue-500 to-indigo-600 flex items-center justify-center font-bold text-white shadow-md shadow-blue-500/20">
            AB
          </div>
          <span class="font-semibold text-white tracking-wide">Abhimanyu Barge</span>
        </div>
        
        <div class="hidden md:flex items-center gap-6 text-sm text-slate-300">
          <a href="#about" class="hover:text-blue-400 transition-colors font-medium">About</a>
          <a href="#experience" class="hover:text-blue-400 transition-colors font-medium">Experience</a>
          <a href="#skills" class="hover:text-blue-400 transition-colors font-medium">Skills</a>
          <a href="#education" class="hover:text-blue-400 transition-colors font-medium">Education</a>
          <button @click="triggerPrint" class="px-4 py-2 rounded-xl bg-slate-800 hover:bg-slate-700 text-blue-400 border border-slate-700 hover:border-slate-600 transition-all font-semibold cursor-pointer">
            PDF Version
          </button>
        </div>
      </div>
    </nav>

    <!-- Main Container -->
    <main class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-8 md:py-16 space-y-12">
      
      <!-- Resume Header Section -->
      <ResumeHeader 
        :name="resumeData.name" 
        :title="resumeData.title" 
        :contact="resumeData.contact" 
      />

      <!-- About Section -->
      <ResumeAbout 
        id="about" 
        :summary="resumeData.summary" 
      />

      <!-- Experience Section -->
      <ResumeExperience 
        id="experience" 
        :experience="resumeData.experience" 
      />

      <!-- Skills Section -->
      <ResumeSkills 
        id="skills" 
        :skills="resumeData.skills" 
      />

      <!-- Education Section -->
      <ResumeEducation 
        id="education" 
        :education="resumeData.education" 
        :courses="resumeData.courses" 
      />

      <!-- Footer & Download PDF Section -->
      <footer class="text-center pt-8 border-t border-slate-800/80">
        <p class="text-sm text-slate-500">
          Designed and built with Vue 3 and Tailwind CSS.
        </p>
        <DownloadButton />
      </footer>
    </main>

    <!-- Scroll to Top Button -->
    <button 
      v-show="showScrollTop"
      @click="scrollToTop"
      class="fixed bottom-6 left-6 z-50 p-3.5 rounded-full bg-slate-800 text-slate-300 hover:text-white border border-slate-700 shadow-xl cursor-pointer hover:scale-110 active:scale-95 transition-all"
      aria-label="Scroll to top">
      <ArrowUp class="h-5 w-5" />
    </button>
  </div>

  <!-- Print Layout (Optimized for single A4 page, only visible on print) -->
  <div class="hidden print:grid resume-print-layout font-sans">
    
    <!-- Print Header -->
    <div class="print-header">
      <div class="print-header-top">
        <div>
          <h1 class="print-name">{{ resumeData.name }}</h1>
          <h2 class="print-title">{{ resumeData.title }}</h2>
        </div>
        <div class="print-contact-grid">
          <div><strong>Phone:</strong> {{ resumeData.contact.phone }}</div>
          <div><strong>Email:</strong> {{ resumeData.contact.email }}</div>
          <div><strong>Location:</strong> {{ resumeData.contact.location }}</div>
          <div><strong>LinkedIn:</strong> linkedin.com/in/abhimanyu-barge</div>
          <div class="col-span-2"><strong>GitHub:</strong> github.com/abhimanyubarge</div>
        </div>
      </div>
    </div>

    <!-- Left Column (Main Content - 7/11 width) -->
    <div class="print-col-main">
      
      <!-- Summary -->
      <div class="print-section">
        <h3 class="print-section-title">Professional Summary</h3>
        <p class="text-[7.6pt] text-slate-700 leading-relaxed">
          {{ resumeData.summary }}
        </p>
      </div>

      <!-- Experience -->
      <div class="print-section">
        <h3 class="print-section-title">Employment History</h3>
        <div class="print-timeline">
          <div v-for="(exp, idx) in resumeData.experience" :key="idx" class="print-timeline-item">
            <div class="print-role-header">
              <span class="print-role-title">
                <strong>{{ exp.role }}</strong> &middot; <span class="print-company">{{ exp.company }}</span>
              </span>
              <span class="print-period">{{ exp.period }}</span>
            </div>
            
            <div v-for="(proj, pIdx) in exp.projects" :key="pIdx" class="print-project">
              <div class="print-role-header">
                <span class="print-project-title">Project: {{ proj.name }} <span v-if="proj.client" class="text-[7pt] font-normal text-slate-500">({{ proj.client }})</span></span>
              </div>
              <p class="print-project-desc text-[7pt] text-slate-600 italic">
                {{ proj.description }}
              </p>
              <ul class="print-bullet-list">
                <!-- Limit printed bullets to fit exactly 1 A4 page -->
                <li v-for="(role, rIdx) in proj.roles.slice(0, 3)" :key="rIdx">
                  {{ role }}
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>

    </div>

    <!-- Right Column (Sidebar - 4/11 width) -->
    <div class="print-col-side">
      
      <!-- Skills -->
      <div class="print-section">
        <h3 class="print-section-title">Skills</h3>
        <div class="space-y-2">
          <div v-for="cat in ['Languages', 'DevOps & Cloud', 'Database', 'Tools']" :key="cat">
            <h4 class="text-[7pt] font-bold text-slate-500 uppercase tracking-wider mb-1">{{ cat }}</h4>
            <div class="print-skills-wrap">
              <span v-for="s in resumeData.skills.filter(sk => sk.category === cat)" :key="s.name" class="print-skill-badge">
                {{ s.name }}
              </span>
            </div>
          </div>
        </div>
      </div>

      <!-- Education -->
      <div class="print-section">
        <h3 class="print-section-title">Education</h3>
        <div class="space-y-2">
          <div v-for="(edu, idx) in resumeData.education" :key="idx" class="print-edu-item">
            <div class="print-edu-title">{{ edu.degree }}</div>
            <div class="print-edu-school">
              <span>{{ edu.institution }}</span>
              <span class="print-period">{{ edu.period.split(' ').pop() }}</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Certifications -->
      <div class="print-section">
        <h3 class="print-section-title">Courses & Training</h3>
        <div class="print-course-grid">
          <div v-for="(course, idx) in resumeData.courses" :key="idx" class="print-course-item">
            &bull; {{ course.name }}
          </div>
        </div>
      </div>

    </div>

  </div>
</template>
