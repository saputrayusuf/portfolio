<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'

const cursor = ref(null)
const cursorOuter = ref(null)

const mouse = { x: 0, y: 0 }
const pos = { x: 0, y: 0 }
const ratio = 0.15 // Lag effect speed for the outer circle

const updatePosition = (e) => {
  mouse.x = e.clientX
  mouse.y = e.clientY
  
  // Instant movement for the small dot
  gsap.set(cursor.value, {
    x: mouse.x,
    y: mouse.y
  })
}

const render = () => {
  // Smoothly interpolate the outer circle's position
  pos.x += (mouse.x - pos.x) * ratio
  pos.y += (mouse.y - pos.y) * ratio
  
  if (cursorOuter.value) {
    gsap.set(cursorOuter.value, {
      x: pos.x,
      y: pos.y
    })
  }
  
  requestAnimationFrame(render)
}

const handleHover = () => {
  gsap.to(cursor.value, {
    scale: 0,
    opacity: 0,
    duration: 0.3,
    ease: 'power2.out'
  })
  gsap.to(cursorOuter.value, {
    scale: 4,
    borderWidth: '1px',
    borderColor: 'rgba(14, 165, 233, 0.5)',
    backgroundColor: 'rgba(14, 165, 233, 0.05)',
    duration: 0.4,
    ease: 'power3.out'
  })
}

const handleLeave = () => {
  gsap.to(cursor.value, {
    scale: 1,
    opacity: 1,
    duration: 0.3,
    ease: 'power2.out'
  })
  gsap.to(cursorOuter.value, {
    scale: 1,
    borderWidth: '1.5px',
    borderColor: 'rgba(14, 165, 233, 0.5)',
    backgroundColor: 'transparent',
    duration: 0.4,
    ease: 'power3.out'
  })
}

onMounted(() => {
  window.addEventListener('mousemove', updatePosition)
  requestAnimationFrame(render)
  
  // Use event delegation for better performance and robustness
  const setupInteractions = () => {
    const interactibles = document.querySelectorAll('a, button, .skill-card, .project-card, .exp-item')
    interactibles.forEach(el => {
      el.addEventListener('mouseenter', handleHover)
      el.addEventListener('mouseleave', handleLeave)
    })
  }

  // Initial setup
  setupInteractions()
  
  // Optional: Re-run if content changes dramatically (simplified here)
  const observer = new MutationObserver(setupInteractions)
  observer.observe(document.body, { childList: true, subtree: true })
})

onUnmounted(() => {
  window.removeEventListener('mousemove', updatePosition)
})
</script>

<template>
  <div class="hidden lg:block pointer-events-none">
    <!-- Smooth Small Dot -->
    <div 
      ref="cursor" 
      class="fixed w-1.5 h-1.5 bg-primary rounded-full pointer-events-none z-[10000] -translate-x-1/2 -translate-y-1/2 shadow-[0_0_10px_rgba(14,165,233,0.8)]"
    ></div>
    
    <!-- Sophisticated Outer Ring -->
    <div 
      ref="cursorOuter" 
      class="fixed w-10 h-10 border-[1.5px] border-primary/40 rounded-full pointer-events-none z-[9999] -translate-x-1/2 -translate-y-1/2 will-change-transform"
    ></div>
  </div>
</template>

<style scoped>
/* Ensure no flickering and high performance */
.fixed {
  backface-visibility: hidden;
  transform-style: preserve-3d;
}
</style>
