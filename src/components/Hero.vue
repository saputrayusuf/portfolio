<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'
import { ChevronRight, Github, Linkedin, Twitter } from 'lucide-vue-next'

const heroTitle = ref(null)
const heroSubtitle = ref(null)
const heroButtons = ref(null)

const typingText = ref('')
const fullText = 'Yusuf Saputra'
const typeSpeed = 150
const pauseEnd = 2000 // Pause before re-typing

const startTyping = () => {
  let isErasing = false
  let i = 0
  
  const type = () => {
    const currentText = fullText
    
    if (!isErasing && i <= currentText.length) {
      typingText.value = currentText.substring(0, i)
      i++
      setTimeout(type, typeSpeed)
    } else if (isErasing && i >= 0) {
      typingText.value = currentText.substring(0, i)
      i--
      setTimeout(type, typeSpeed / 2)
    } else if (i > currentText.length) {
      isErasing = true
      setTimeout(type, pauseEnd)
    } else {
      isErasing = false
      i = 0
      setTimeout(type, 500)
    }
  }
  
  type()
}

onMounted(() => {
  const tl = gsap.timeline()
  
  startTyping()

  tl.from(heroTitle.value, {
    y: 100,
    opacity: 0,
    duration: 1,
    ease: 'power4.out',
    delay: 0.5
  })
  .from(heroSubtitle.value, {
    y: 50,
    opacity: 0,
    duration: 0.8,
    ease: 'power3.out'
  }, '-=0.6')
  .from(heroButtons.value, {
    y: 30,
    opacity: 0,
    duration: 0.8,
    ease: 'power2.out'
  }, '-=0.4')
  
  // Floating animation for the background element
  gsap.to('.hero-shape', {
    y: 20,
    duration: 2,
    repeat: -1,
    yoyo: true,
    ease: 'sine.inOut'
  })
})
</script>

<template>
  <section id="home" class="relative min-h-screen flex items-center justify-center pt-20 overflow-hidden">
    <!-- Animated background shapes -->
    <div class="absolute top-1/4 left-1/4 w-96 h-96 bg-primary/20 rounded-full blur-[120px] hero-shape"></div>
    <div class="absolute bottom-1/4 right-1/4 w-[500px] h-[500px] bg-secondary/10 rounded-full blur-[150px] hero-shape" style="animation-delay: -1s"></div>

    <div class="max-w-7xl mx-auto px-6 relative z-10 text-center">
      <div 
        ref="heroTitle" 
        class="mb-6"
      >
        <span class="inline-block px-4 py-1.5 mb-4 text-xs font-bold tracking-widest uppercase text-primary border border-primary/30 rounded-full bg-primary/5">
          Tersedia untuk Proyek Baru
        </span>
        <h1 class="text-5xl md:text-7xl font-black mb-6 leading-tight min-h-[1.2em]">
          Saya <span class="bg-gradient-to-r from-primary via-secondary to-accent bg-clip-text text-transparent">
            {{ typingText }}
          </span>
          <span class="inline-block w-[4px] h-[0.8em] bg-primary ml-1 animate-pulse"></span>
        </h1>
      </div>

      <p 
        ref="heroSubtitle"
        class="text-lg md:text-xl text-gray-400 max-w-2xl mx-auto mb-10 font-light"
      >
        Pengembang Web dan Mobile yang fokus pada solusi Fullstack menggunakan teknologi modern seperti CodeIgniter, Angular, dan Flutter.
      </p>

      <div 
        ref="heroButtons"
        class="flex flex-col sm:flex-row items-center justify-center gap-4"
      >
        <a 
          href="#projects" 
          class="group px-8 py-4 bg-primary text-white rounded-xl font-bold flex items-center gap-2 hover:bg-primary/90 transition-all hover:scale-105 active:scale-95 shadow-lg shadow-primary/20"
        >
          Lihat Karya Saya
          <ChevronRight class="group-hover:translate-x-1 transition-transform" />
        </a>
        
        <div class="flex items-center gap-4 ml-0 sm:ml-4">
          <a href="#" class="p-3 glass rounded-full hover:text-primary transition-colors border-white/5">
            <Github :size="20" />
          </a>
          <a href="#" class="p-3 glass rounded-full hover:text-primary transition-colors border-white/5">
            <Linkedin :size="20" />
          </a>
          <a href="#" class="p-3 glass rounded-full hover:text-primary transition-colors border-white/5">
            <Twitter :size="20" />
          </a>
        </div>
      </div>
    </div>
    
    <!-- Scroll indicator -->
    <div class="absolute bottom-10 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 opacity-50">
      <span class="text-[10px] uppercase tracking-widest font-bold">Scroll</span>
      <div class="w-[1px] h-12 bg-gradient-to-b from-primary to-transparent"></div>
    </div>
  </section>
</template>
