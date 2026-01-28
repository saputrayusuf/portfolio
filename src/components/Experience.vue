<script setup>
import { onMounted } from 'vue'
import gsap from 'gsap'
import { Briefcase, Calendar } from 'lucide-vue-next'

const experiences = [
  {
    company: 'PT. Bangun Putra Pesaka',
    role: 'Fullstack Developer',
    period: 'Okt 2021 - Sekarang',
    description: 'Membangun ekosistem digital yang kompleks, termasuk integrasi GPS tracking dengan ERP, dashboard visualisasi data logistik secara real-time, serta sistem absensi berbasis Face Detection untuk efisiensi operasional.',
    tech: ['CodeIgniter 4', 'Ext JS', 'Flutter', 'Angular', 'MySQL']
  },
  {
    company: 'PT. Semar Gadai Setiai',
    role: 'Software Developer',
    period: 'Jun 2021 - Okt 2021',
    description: 'Mengembangkan sistem inti layanan pegadaian, aplikasi strategi promosi retail, serta modul pelaporan keuangan terintegrasi untuk mendukung akurasi data finansial.',
    tech: ['.Net Framework', 'MariaDB']
  }
]

onMounted(() => {
  gsap.from('.exp-item', {
    scrollTrigger: {
      trigger: '#experience',
      start: 'top 80%',
    },
    x: -50,
    opacity: 0,
    duration: 0.8,
    stagger: 0.2,
    ease: 'power3.out'
  })
})
</script>

<template>
  <section id="experience" class="py-24 relative overflow-hidden">
    <div class="max-w-7xl mx-auto px-6 relative z-10">
      <div class="flex flex-col md:flex-row md:items-end justify-between mb-16 gap-6">
        <div>
          <h2 class="text-4xl md:text-5xl font-bold mb-4 text-white">
            Pengalaman <span class="bg-gradient-to-r from-primary to-secondary bg-clip-text text-transparent italic">Kerja</span>
          </h2>
          <div class="w-20 h-1.5 bg-secondary rounded-full"></div>
        </div>
        <p class="text-gray-400 max-w-md">
          Perjalanan profesional saya dalam membangun berbagai solusi perangkat lunak yang kompleks.
        </p>
      </div>

      <div class="relative">
        <!-- Vertical Line -->
        <div class="absolute left-0 md:left-1/2 top-0 bottom-0 w-px bg-white/10 -translate-x-1/2 hidden md:block"></div>

        <div class="space-y-12">
          <div 
            v-for="(exp, index) in experiences" 
            :key="exp.company"
            :class="['exp-item relative flex flex-col md:flex-row gap-8 md:gap-0', index % 2 === 0 ? 'md:flex-row-reverse' : '']"
          >
            <!-- Timeline Dot -->
            <div class="absolute left-0 md:left-1/2 top-0 w-4 h-4 bg-primary rounded-full shadow-[0_0_15px_rgba(14,165,233,0.5)] -translate-x-1/2 z-20 hidden md:block"></div>

            <!-- Content Side -->
            <div class="w-full md:w-1/2 px-0 md:px-12">
              <div class="glass p-8 rounded-3xl border-white/5 hover:border-primary/30 transition-all duration-500">
                <div class="flex items-center gap-2 text-primary mb-4">
                  <Calendar :size="16" />
                  <span class="text-sm font-bold uppercase tracking-widest">{{ exp.period }}</span>
                </div>
                <h3 class="text-2xl font-bold mb-1 text-white">{{ exp.role }}</h3>
                <p class="text-lg text-primary/80 font-medium mb-4 flex items-center gap-2">
                  <Briefcase :size="18" /> {{ exp.company }}
                </p>
                <p class="text-gray-400 mb-6 leading-relaxed">
                  {{ exp.description }}
                </p>
                <div class="flex flex-wrap gap-2">
                  <span 
                    v-for="t in exp.tech" 
                    :key="t"
                    class="text-[10px] px-3 py-1 rounded-full bg-white/5 text-gray-300 font-bold border border-white/10"
                  >
                    {{ t }}
                  </span>
                </div>
              </div>
            </div>
            
            <!-- Spacer Side -->
            <div class="w-full md:w-1/2"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
