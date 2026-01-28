<script setup>
import { onMounted } from 'vue'
import gsap from 'gsap'
import { 
  FileCode,   // PHP
  Code2,      // Angular
  Smartphone, // Flutter
  ScrollText, // Javascript
  Wind,       // CodeIgniter
  LayoutGrid, // Ext JS
  Database    // MySQL
} from 'lucide-vue-next'

const skills = [
  { 
    name: 'PHP', 
    icon: FileCode, 
    color: 'text-indigo-500', 
    borderColor: 'border-indigo-500/50',
    desc: 'Pengembangan backend yang solid dan modular sebagai basis utama berbagai aplikasi web enterprise.',
    tags: ['OOP', 'MVC', 'Security']
  },
  { 
    name: 'Javascript', 
    icon: ScrollText, 
    color: 'text-yellow-400', 
    borderColor: 'border-yellow-400/50',
    desc: 'Interpretasi logika kompleks di sisi klien dan server untuk menciptakan interaksi yang dinamis dan modern.',
    tags: ['ES6+', 'DOM', 'Asynchronous']
  },
  { 
    name: 'CodeIgniter 4', 
    icon: Wind, 
    color: 'text-red-500', 
    borderColor: 'border-red-500/50',
    desc: 'Membangun aplikasi web yang cepat, ringan, dan aman menggunakan framework CI4.',
    tags: ['PHP', 'MVC', 'RESTful']
  },
  { 
    name: 'Angular', 
    icon: Code2, 
    color: 'text-red-500', 
    borderColor: 'border-red-500/50',
    desc: 'Spesialis dalam pengembangan SPA (Single Page Application) skala besar yang kompleks.',
    tags: ['TypeScript', 'RxJS', 'Signals']
  },
  { 
    name: 'Flutter', 
    icon: Smartphone, 
    color: 'text-blue-500', 
    borderColor: 'border-blue-500/50',
    desc: 'Membuat aplikasi mobile berperforma tinggi untuk Android dan iOS dengan satu basis kode.',
    tags: ['Dart', 'Widgets', 'Material UI']
  },
  { 
    name: 'Ext JS', 
    icon: LayoutGrid, 
    color: 'text-green-500', 
    borderColor: 'border-green-500/50',
    desc: 'Pengembangan interface data-intensive untuk kebutuhan aplikasi bisnis dan enterprise.',
    tags: ['Sencha', 'Grid', 'Modern Toolkit']
  },
  { 
    name: 'MySQL', 
    icon: Database, 
    color: 'text-cyan-500', 
    borderColor: 'border-cyan-500/50',
    desc: 'Manajemen dan optimasi basis data relasional untuk integritas data tingkat tinggi.',
    tags: ['SQL', 'Optimasi', 'RDBMS']
  }
]

onMounted(() => {
  // Animasi masuk yang lebih dinamis dan premium
  gsap.from('.skill-card', {
    scrollTrigger: {
      trigger: '#skills',
      start: 'top 70%',
      toggleActions: 'play none none none',
    },
    y: 60,
    scale: 0.9,
    opacity: 0,
    rotateX: -15,
    duration: 0.8,
    stagger: {
      amount: 0.4,
      from: "start"
    },
    ease: 'power4.out',
    clearProps: 'all' // Membersihkan props setelah animasi selesai agar hover tetap lancar
  })
})
</script>

<template>
  <section id="skills" class="py-24 relative overflow-hidden bg-dark">
    <!-- Dekorasi background konsisten -->
    <div class="absolute top-1/4 right-1/4 w-96 h-96 bg-primary/10 rounded-full blur-[120px]"></div>
    <div class="absolute bottom-1/4 left-1/4 w-[500px] h-[500px] bg-secondary/5 rounded-full blur-[150px]"></div>

    <div class="max-w-7xl mx-auto px-6 relative z-10">
      <div class="flex flex-col md:flex-row md:items-end justify-between mb-16 gap-6">
        <div>
          <h2 class="text-4xl md:text-5xl font-bold mb-4 text-white">
            Keahlian <span class="bg-gradient-to-r from-primary to-secondary bg-clip-text text-transparent italic">Teknis</span>
          </h2>
          <div class="w-20 h-1.5 bg-primary rounded-full"></div>
        </div>
        <p class="text-gray-400 max-w-md">
          Daftar lengkap teknologi yang saya kuasai untuk membangun solusi digital terbaik.
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <div 
          v-for="skill in skills" 
          :key="skill.name"
          :class="[
            'skill-card group p-8 rounded-2xl bg-[#0f172a] border-2 transition-all duration-300 hover:-translate-y-1 relative overflow-hidden shadow-xl opacity-100',
            skill.borderColor,
            'hover:border-primary/50'
          ]"
        >
          <!-- Ikon Ring -->
          <div :class="['p-4 rounded-xl w-fit mb-6 bg-slate-950 ring-2 transition-all duration-300 relative z-10 shadow-lg', skill.color, skill.borderColor.replace('border-', 'ring-')]">
            <component :is="skill.icon" :size="36" stroke-width="2.5" />
          </div>
          
          <h3 class="text-2xl font-bold mb-3 text-white group-hover:text-primary transition-colors relative z-10">
            {{ skill.name }}
          </h3>
          
          <p class="text-gray-300 text-sm mb-6 leading-relaxed font-medium relative z-10">
            {{ skill.desc }}
          </p>
          
          <div class="flex flex-wrap gap-2 relative z-10">
            <span 
              v-for="tag in skill.tags" 
              :key="tag"
              class="text-[10px] px-3 py-1.5 rounded-lg bg-slate-950 text-white font-bold border border-white/10 group-hover:border-primary/30 transition-all uppercase tracking-widest shadow-sm"
            >
              {{ tag }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Transisi halus untuk hover */
.skill-card {
  perspective: 1000px;
}
</style>
