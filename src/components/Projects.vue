<script setup>
import { ref, computed } from 'vue'
import { ExternalLink, Github, X, CheckCircle2 } from 'lucide-vue-next'

const showAll = ref(false)
const selectedProject = ref(null)

const allProjects = [
  {
    title: 'Smart Attendance',
    subtitle: 'Advanced Face Recognition System',
    description: 'Sistem kehadiran digital cerdas yang memanfaatkan teknologi Face Recognition berbasis AI untuk efisiensi dan akurasi pencatatan absensi.',
    fullDescription: 'Aplikasi manajemen kehadiran modern yang menggabungkan kemudahan aplikasi mobile dengan kekuatan AI. Menggunakan library DeepFace dan backend FastAPI untuk melakukan pengenalan wajah (Face Detection) yang cepat dan akurat. Sistem ini dilengkapi dengan proteksi Anti-Fake GPS, manajemen payroll otomatis, serta fitur pengajuan izin dan cuti secara digital untuk mempermudah manajemen SDM.',
    image: '/projects/attendance-mobile-home.png',
    gallery: ['/projects/attendance-mobile-home.png', '/projects/attendance-mobile-login.png', '/projects/attendance-web-admin.png'],
    tech: ['Flutter', 'FastAPI', 'DeepFace', 'Angular', 'MySQL'],
    features: ['Anti-Fake GPS Protection', 'Automated Payroll System', 'Digital Leave & Permit Submission', 'Microservices Architecture'],
    link: '#',
    github: '#'
  },
  {
    title: 'Smart Security Patrol System',
    subtitle: 'Security Operations Management',
    description: 'Sistem monitoring patroli keamanan real-time dengan integrasi QR Scan, deteksi wajah, dan pelacakan lokasi petugas berbasis GIS.',
    fullDescription: 'Solusi manajemen keamanan modern yang mengintegrasikan aplikasi mobile petugas dan dashboard admin. Petugas melakukan patroli melalui verifikasi QR Code di setiap checkpoint, dilengkapi fitur absensi biometrik wajah dan tombol darurat (Emergency Alert). Dashboard admin menyediakan pemantauan lokasi petugas secara live (Live Tracking), manajemen checkpoint, serta pelaporan otomatis untuk efektivitas pengamanan area.',
    image: '/projects/security-patrol-login.png',
    gallery: [
      '/projects/security-patrol-login.png',
      '/projects/security-patrol-tracking.png',
      '/projects/security-patrol-checkpoints.png',
      '/projects/security-patrol-mobile.png'
    ],
    tech: ['Flutter', 'Laravel', 'Inertia.js', 'Vue.js', 'MySQL'],
    features: [
      'QR Code Checkpoint Scanning',
      'Face Recognition Attendance',
      'Real-time Live GPS Tracking',
      'Emergency Alert System',
      'Operational Incident Reporting'
    ],
    link: '#',
    github: '#'
  },
  {
    title: 'Operational Planner Dashboard',
    subtitle: 'Logistics Resource Planning',
    description: 'Dashboard mobile untuk optimasi pengawasan armada, memantau posisi unit, serta jadwal aktivitas In/Out di area pelabuhan dan depo.',
    fullDescription: 'Aplikasi dashboard strategis yang dirancang khusus untuk tim planner dalam memantau pergerakan armada secara efisien. Fitur utama mencakup monitoring lokasi kendaraan secara berkala, pencatatan waktu masuk dan keluar (In/Out) di area pelabuhan serta depo, hingga visibilitas terhadap tugas operasional yang sedang berjalan. Dibangun untuk memberikan gambaran data operasional yang akurat guna mendukung manajemen logistik yang lebih terstruktur.',
    image: '/projects/planner-dashboard-main.jpg',
    gallery: [
      '/projects/planner-dashboard-main.jpg',
      '/projects/planner-dashboard-menu.jpg'
    ],
    tech: ['Flutter', 'CodeIgniter 4', 'MySQL'],
    features: [
      'Vehicle Location Monitoring',
      'In/Out Port & Depot Tracking',
      'Operational Status Insights',
      'Daily Chart & Summary Analytics'
    ],
    link: '#',
    github: '#'
  },
  {
    title: 'Customer CRM & Container Tracking',
    subtitle: 'Logistics & Supply Chain Solution',
    description: 'Sistem CRM terintegrasi untuk pemantauan order dan pelacakan kontainer secara real-time. Memudahkan koordinasi operasional serta manajemen dokumen ekspor-impor dan logistik domestik dalam satu platform yang efisien.',
    fullDescription: 'Platform CRM & Tracking ini dirancang untuk menjawab tantangan kompleks dalam industri logistik. Fitur utamanya mencakup pelacakan kontainer melalui integrasi API vendor, manajemen siklus hidup order dari reservasi hingga pengiriman, serta sistem manajemen dokumen digital (EDM) untuk file ekspor/impor. Dibangun dengan fokus pada efisiensi operasional dan transparansi data bagi pelanggan.',
    image: '/projects/crm-logistics.png',
    gallery: ['/projects/crm-logistics.png'],
    tech: ['Angular', 'CodeIgniter 4', 'MySQL'],
    features: ['Real-time Container Tracking', 'Document Management (Export/Import)', 'Order Management System', 'Customer Dashboard'],
    link: '#',
    github: '#'
  },
  {
    title: 'Smart Workplace & ERP Ecosystem',
    subtitle: 'Integrated Human Resource System',
    description: 'Solusi manajemen SDM terpadu dengan verifikasi biometrik wajah, proteksi lokasi (Anti-Fake GPS), dan integrasi penuh ke sistem ERP perusahaan.',
    fullDescription: 'Smart Workplace adalah platform manajemen karyawan komprehensif yang menghubungkan aplikasi mobile (Flutter) dengan dashboard admin berbasis Ext JS. Sistem ini meminimalisir kecurangan absensi melalui teknologi deteksi wajah dan proteksi area berbasis GPS (Anti-Fake GPS). Terintegrasi langsung dengan ekosistem ERP, aplikasi ini memudahkan pengelolaan izin/cuti, pelaporan temuan operasional secara instan, serta distribusi notifikasi penting melalui OneSignal guna meningkatkan efisiensi koordinasi internal.',
    image: '/projects/mybpl-home.jpg',
    gallery: [
      '/projects/mybpl-home.jpg',
      '/projects/mybpl-login.jpg',
      '/projects/mybpl-registration.jpg'
    ],
    tech: ['Flutter', 'CodeIgniter 4', 'Ext JS', 'MySQL', 'OneSignal'],
    features: [
      'Face Recognition Attendance',
      'Anti-Fake GPS Protection',
      'Digital Leave & Permit Submission',
      'Operational Finding Reports',
      'OneSignal Push Notifications',
      'Direct ERP Integration'
    ],
    link: '#',
    github: '#'
  },
  {
    title: 'Logistics Visualization Dashboard',
    subtitle: 'Data Analytics & Monitoring',
    description: 'Dashboard interaktif untuk visualisasi metrik operasional secara real-time guna mendukung pengambilan keputusan yang lebih cepat.',
    fullDescription: 'Dashboard analitik yang menyajikan visualisasi data besar dari aktivitas logistik harian. Menampilkan status Unit, Driver, dan Chassis secara live menggunakan peta interaktif dan grafik statistik. Dirancang untuk membantu jajaran manajemen dalam memantau bottleneck operasional dan mengalokasikan sumber daya secara tepat sasaran.',
    image: '/projects/dashboard-kencana.png',
    gallery: ['/projects/dashboard-kencana.png'],
    tech: ['Angular', 'CodeIgniter 4', 'Chart.js', 'Leaflet', 'MySQL'],
    features: ['Operational KPI Visualization', 'Interactive Map Monitoring', 'Inventory Tracking Dashboard', 'Auto-refresh Data Feed'],
    link: '#',
    github: '#'
  },
  {
    title: 'Enterprise ERP Ecosystem',
    subtitle: 'Corporate Core Management System',
    description: 'Sistem ERP terintegrasi untuk efisiensi proses bisnis korporat dengan arsitektur microservices yang skalabel.',
    fullDescription: 'Berkontribusi dalam pengembangan sistem ERP inti perusahaan yang dirancang untuk mengintegrasikan berbagai departemen ke dalam satu platform yang terpusat. Menggunakan Ext JS untuk menyediakan antarmuka admin yang kompleks dan backend berbasis Microservices dengan CodeIgniter 4. Sistem ini mencakup modul operasional, manajemen aset, hingga pelaporan keuangan untuk memastikan sinkronisasi data yang akurat di seluruh divisi.',
    image: '/projects/extjs-erp-generated.png',
    gallery: ['/projects/extjs-erp-generated.png'],
    tech: ['Ext JS', 'CodeIgniter 4', 'Microservices', 'MySQL'],
    features: [
      'Modular Business Logic',
      'Scalable Microservices Architecture',
      'Advanced Corporate Reporting',
      'Enterprise Data Synchronization'
    ],
    link: '#',
    github: '#'
  },
  {
    title: 'Corporate Branding & Landing Page',
    subtitle: 'Business Digital Presence',
    description: 'Landing page korporat yang responsif dan elegan untuk memperkuat identitas brand serta konversi layanan bisnis.',
    fullDescription: 'Pengembangan website landing page profesional yang dirancang untuk meningkatkan kehadiran digital perusahaan. Dibangun dengan framework Laravel, platform ini fokus pada user experience yang mulus dan kemudahan konversi. Dilengkapi dengan integrasi form kontak direct-to-email serta tombol interaktif yang terhubung langsung ke WhatsApp untuk memudahkan calon klien dalam menjalin komunikasi bisnis secara instan.',
    image: '/projects/landing-page-hero.png',
    gallery: [
      '/projects/landing-page-hero.png',
      '/projects/landing-page-product.png'
    ],
    tech: ['Laravel', 'Blade', 'Bootstrap', 'MySQL'],
    features: [
      'Responsive Corporate Design',
      'SMTP Email Integration',
      'WhatsApp Business Integration',
      'Dynamic Product Showcase'
    ],
    link: '#',
    github: '#'
  }
]

const displayedProjects = computed(() => {
  return showAll.value ? allProjects : allProjects.slice(0, 3)
})

const openProject = (project) => {
  selectedProject.value = project
  document.body.style.overflow = 'hidden'
}

const closeProject = () => {
  selectedProject.value = null
  document.body.style.overflow = 'auto'
}

import { onMounted } from 'vue'
import gsap from 'gsap'

onMounted(() => {
  gsap.from('.project-card', {
    scrollTrigger: {
      trigger: '#projects',
      start: 'top 80%',
    },
    y: 50,
    opacity: 0,
    duration: 0.8,
    stagger: 0.1,
    ease: 'power2.out'
  })
})
</script>

<template>
  <section id="projects" class="py-24 relative overflow-hidden">
    <div class="max-w-7xl mx-auto px-6">
      <div class="flex flex-col md:flex-row md:items-end justify-between mb-16 gap-6">
        <div>
          <h2 class="text-4xl md:text-5xl font-bold mb-4">
            Karya <span class="bg-gradient-to-r from-primary to-secondary bg-clip-text text-transparent italic">Unggulan</span>
          </h2>
          <div class="w-20 h-1.5 bg-secondary rounded-full"></div>
        </div>
        <p class="text-gray-400 max-w-md">
          Eksplorasi portofolio project profesional saya dalam pengembangan sistem enterprise yang kompleks dan skalabel.
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <TransitionGroup 
          name="list"
          enter-active-class="transition-all duration-500 ease-out"
          enter-from-class="opacity-0 translate-y-10"
          enter-to-class="opacity-100 translate-y-0"
        >
          <div 
            v-for="project in displayedProjects" 
            :key="project.title"
            class="project-card group relative h-[450px] overflow-hidden rounded-3xl cursor-pointer"
            @click="openProject(project)"
          >
            <!-- Background Image -->
            <img 
              :src="project.image" 
              :alt="project.title"
              class="absolute inset-0 w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"
            >
            
            <!-- Overlay -->
            <div class="absolute inset-0 bg-gradient-to-t from-dark via-dark/60 to-transparent transition-opacity duration-500 opacity-90 group-hover:opacity-100"></div>
            
            <!-- Content -->
            <div class="absolute inset-0 p-8 flex flex-col justify-end">
              <div class="flex flex-wrap gap-2 mb-4">
                <span 
                  v-for="item in project.tech.slice(0, 3)" 
                  :key="item"
                  class="px-3 py-1 text-[10px] font-bold bg-white/10 backdrop-blur-md rounded-full border border-white/10"
                >
                  {{ item }}
                </span>
                <span v-if="project.tech.length > 3" class="px-3 py-1 text-[10px] font-bold bg-white/10 backdrop-blur-md rounded-full border border-white/10">
                  +{{ project.tech.length - 3 }}
                </span>
              </div>
              
              <h3 class="text-2xl font-bold mb-1 group-hover:text-primary transition-colors">{{ project.title }}</h3>
              <p class="text-sm text-gray-400 mb-4">{{ project.subtitle }}</p>
              
              <p class="text-gray-300 text-sm mb-6 line-clamp-2 opacity-0 group-hover:opacity-100 transition-all duration-300 translate-y-4 group-hover:translate-y-0">
                {{ project.description }}
              </p>
              
              <div class="flex items-center gap-4 opacity-0 group-hover:opacity-100 transition-all duration-300 translate-y-4 group-hover:translate-y-0 delay-100">
                <span class="text-sm font-bold text-primary flex items-center gap-2">
                  Lihat Detail <ExternalLink :size="16" />
                </span>
              </div>
            </div>
          </div>
        </TransitionGroup>
      </div>
      
      <div class="mt-16 text-center">
        <button 
          @click="showAll = !showAll"
          class="px-8 py-3 glass rounded-xl border-white/10 font-bold hover:bg-white/10 transition-colors"
        >
          {{ showAll ? 'Tampilkan Unggulan Saja' : 'Lihat Semua Proyek' }}
        </button>
      </div>
    </div>

    <!-- Modal -->
    <Transition name="fade">
      <div v-if="selectedProject" class="fixed inset-0 z-[100] flex items-center justify-center p-4 md:p-8">
        <div class="absolute inset-0 bg-dark/95 backdrop-blur-md" @click="closeProject"></div>
        
        <div class="relative w-full max-w-5xl max-h-[90vh] bg-dark-secondary rounded-3xl border border-white/10 overflow-hidden flex flex-col md:flex-row shadow-2xl">
          <button 
            @click="closeProject"
            class="absolute top-4 right-4 z-10 w-10 h-10 flex items-center justify-center rounded-full bg-dark/50 border border-white/10 hover:bg-white/10 transition-colors"
          >
            <X :size="20" />
          </button>

          <!-- Modal Left: Gallery -->
          <div class="w-full md:w-1/2 h-64 md:h-auto overflow-y-auto bg-dark p-6 space-y-4">
            <img 
              v-for="(img, idx) in selectedProject.gallery" 
              :key="idx"
              :src="img" 
              :alt="selectedProject.title"
              class="w-full rounded-2xl shadow-lg border border-white/5"
            >
          </div>

          <!-- Modal Right: Details -->
          <div class="w-full md:w-1/2 p-8 md:p-12 overflow-y-auto bg-gradient-to-br from-dark-secondary to-dark">
            <div class="flex flex-wrap gap-2 mb-6">
              <span 
                v-for="tech in selectedProject.tech" 
                :key="tech"
                class="px-3 py-1 text-[11px] font-bold bg-primary/10 text-primary border border-primary/20 rounded-full"
              >
                {{ tech }}
              </span>
            </div>

            <h3 class="text-3xl font-bold mb-2">{{ selectedProject.title }}</h3>
            <p class="text-primary font-medium mb-6">{{ selectedProject.subtitle }}</p>
            
            <div class="space-y-6">
              <div>
                <h4 class="text-white font-bold mb-2 flex items-center gap-2">
                  Project Overview
                </h4>
                <p class="text-gray-400 text-sm leading-relaxed">
                  {{ selectedProject.fullDescription }}
                </p>
              </div>

              <div>
                <h4 class="text-white font-bold mb-3 flex items-center gap-2">
                  Key Features
                </h4>
                <ul class="grid grid-cols-1 gap-2">
                  <li v-for="feature in selectedProject.features" :key="feature" class="flex items-start gap-2 text-sm text-gray-400">
                    <CheckCircle2 :size="16" class="text-primary mt-0.5 shrink-0" />
                    {{ feature }}
                  </li>
                </ul>
              </div>

              <div class="flex items-center gap-4 pt-4">
                <a :href="selectedProject.link" class="flex-1 px-6 py-3 bg-primary text-white font-bold rounded-xl text-center hover:opacity-90 transition-opacity flex items-center justify-center gap-2">
                  <ExternalLink :size="18" /> Demo
                </a>
                <a :href="selectedProject.github" class="flex-1 px-6 py-3 glass border-white/10 text-white font-bold rounded-xl text-center hover:bg-white/10 transition-colors flex items-center justify-center gap-2">
                  <Github :size="18" /> Source
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </Transition>
  </section>
</template>

<style scoped>
.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.list-leave-active {
  position: absolute;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* Custom Scrollbar for Modal content */
::-webkit-scrollbar {
  width: 6px;
}
::-webkit-scrollbar-track {
  background: transparent;
}
::-webkit-scrollbar-thumb {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
}
::-webkit-scrollbar-thumb:hover {
  background: rgba(255, 255, 255, 0.2);
}
</style>
