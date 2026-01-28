<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const canvasRef = ref(null)
let ctx = null
let animationFrameId = null
let particles = []

class Particle {
  constructor(w, h) {
    this.w = w
    this.h = h
    this.reset()
  }

  reset() {
    this.x = Math.random() * this.w
    this.y = Math.random() * this.h
    this.size = Math.random() * 2
    this.speedX = (Math.random() - 0.5) * 0.5
    this.speedY = (Math.random() - 0.5) * 0.5
    this.opacity = Math.random() * 0.5
  }

  update() {
    this.x += this.speedX
    this.y += this.speedY

    if (this.x < 0 || this.x > this.w || this.y < 0 || this.y > this.h) {
      this.reset()
    }
  }

  draw() {
    ctx.fillStyle = `rgba(14, 165, 233, ${this.opacity})`
    ctx.beginPath()
    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2)
    ctx.fill()
  }
}

const init = () => {
  const canvas = canvasRef.value
  ctx = canvas.getContext('2d')
  
  const resize = () => {
    canvas.width = window.innerWidth
    canvas.height = window.innerHeight
    particles = Array.from({ length: 100 }, () => new Particle(canvas.width, canvas.height))
  }

  window.addEventListener('resize', resize)
  resize()

  const animate = () => {
    ctx.clearRect(0, 0, canvas.width, canvas.height)
    particles.forEach(p => {
      p.update()
      p.draw()
    })
    animationFrameId = requestAnimationFrame(animate)
  }

  animate()
}

onMounted(() => {
  init()
})

onUnmounted(() => {
  cancelAnimationFrame(animationFrameId)
})
</script>

<template>
  <canvas 
    ref="canvasRef" 
    class="fixed inset-0 pointer-events-none z-0"
  ></canvas>
</template>
