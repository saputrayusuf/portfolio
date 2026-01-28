<script setup>
import { ref, onMounted } from 'vue'
import { Menu, X, Rocket } from 'lucide-vue-next'

const isMenuOpen = ref(false)
const scrolled = ref(false)

onMounted(() => {
  window.addEventListener('scroll', () => {
    scrolled.value = window.scrollY > 50
  })
})

const navLinks = [
  { name: 'Beranda', href: '#home' },
  { name: 'Keahlian', href: '#skills' },
  { name: 'Pengalaman', href: '#experience' },
  { name: 'Proyek', href: '#projects' },
  { name: 'Kontak', href: '#contact' }
]
</script>

<template>
  <nav 
    :class="[
      'fixed w-full z-50 transition-all duration-300 px-6 py-4',
      scrolled ? 'bg-dark/80 backdrop-blur-md border-b border-white/10 py-3' : 'bg-transparent'
    ]"
  >
    <div class="max-w-7xl mx-auto flex justify-between items-center">
      <div class="flex items-center space-x-2 group cursor-pointer font-mono font-bold text-xl">
        <Rocket class="text-primary group-hover:animate-bounce" :size="28" />
        <span class="bg-gradient-to-r from-primary to-secondary bg-clip-text text-transparent">
          YUSUF.DEV
        </span>
      </div>

      <!-- Desktop Nav -->
      <div class="hidden md:flex items-center space-x-8">
        <a 
          v-for="link in navLinks" 
          :key="link.name" 
          :href="link.href"
          class="text-sm font-medium hover:text-primary transition-colors duration-200"
        >
          {{ link.name }}
        </a>
        <a 
          href="#contact" 
          class="px-5 py-2 rounded-full bg-primary/10 border border-primary/50 text-primary hover:bg-primary hover:text-white transition-all duration-300"
        >
          Hubungi Saya
        </a>
      </div>

      <!-- Mobile Menu Toggle -->
      <button class="md:hidden text-white" @click="isMenuOpen = !isMenuOpen">
        <Menu v-if="!isMenuOpen" :size="28" />
        <X v-else :size="28" />
      </button>
    </div>

    <!-- Mobile Nav -->
    <div 
      v-if="isMenuOpen" 
      class="md:hidden absolute top-full left-0 w-full bg-dark/95 backdrop-blur-lg border-b border-white/10 py-6 px-6 space-y-4"
    >
      <a 
        v-for="link in navLinks" 
        :key="link.name" 
        :href="link.href"
        @click="isMenuOpen = false"
        class="block text-lg font-medium hover:text-primary"
      >
        {{ link.name }}
      </a>
      <a 
        href="#contact" 
        @click="isMenuOpen = false"
        class="block w-full text-center py-3 rounded-lg bg-primary text-white font-bold"
      >
        Hubungi Saya
      </a>
    </div>
  </nav>
</template>
