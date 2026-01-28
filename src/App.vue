<script setup>
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import Skills from './components/Skills.vue'
import Experience from './components/Experience.vue'
import Projects from './components/Projects.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
import ParticleBackground from './components/ParticleBackground.vue'
import CustomCursor from './components/CustomCursor.vue'
import { onMounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  // Global animations if any
})
</script>

<template>
  <div class="min-h-screen bg-dark overflow-x-hidden">
    <CustomCursor />
    <ParticleBackground />
    
    <Navbar />
    <main>
      <Hero />
      <Skills />
      <Experience />
      <Projects />
      <Contact />
    </main>
    <Footer />
  </div>
</template>

<style>
/* Custom cursor or other global styles */
::-webkit-scrollbar {
  width: 8px;
}
::-webkit-scrollbar-track {
  background: #0f172a;
}
::-webkit-scrollbar-thumb {
  background: #0ea5e9;
  border-radius: 4px;
}
::-webkit-scrollbar-thumb:hover {
  background: #6366f1;
}
</style>
