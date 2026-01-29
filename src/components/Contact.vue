<script setup>
import { reactive, onMounted } from 'vue'
import { Send, Mail, MapPin, Phone } from 'lucide-vue-next'
import gsap from 'gsap'

const form = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const handleSubmit = () => {
  const mailtoLink = `mailto:dummy@example.com?subject=${encodeURIComponent(form.subject || 'Pertanyaan Proyek')} dari ${encodeURIComponent(form.name)}&body=${encodeURIComponent(form.message)}%0D%0A%0D%0ABalas ke: ${form.email}`
  window.location.href = mailtoLink
}

onMounted(() => {
  gsap.from('.contact-animate', {
    scrollTrigger: {
      trigger: '#contact',
      start: 'top 80%',
    },
    x: (i) => i === 0 ? -50 : 50,
    opacity: 0,
    duration: 1,
    ease: 'power3.out'
  })
})
</script>

<template>
  <section id="contact" class="py-24 bg-dark/50">
    <div class="max-w-7xl mx-auto px-6">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-16">
        <div class="contact-animate">
          <h2 class="text-4xl md:text-5xl font-bold mb-6">
            Hubungi <span class="text-accent italic">Saya</span>
          </h2>
          <p class="text-gray-400 mb-10 text-lg">
            Punya proyek dalam pikiran? Mari bangun sesuatu yang luar biasa bersama. Hubungi saya melalui formulir atau kontak langsung.
          </p>
          
          <div class="space-y-6">
            <div class="flex items-center gap-4">
              <div class="p-3 glass rounded-lg text-primary border-white/5">
                <Mail :size="24" />
              </div>
              <div>
                <p class="text-xs text-gray-500 uppercase font-bold tracking-widest">Email</p>
                <p class="text-lg font-medium font-mono">saputrayusuf133@gmail.com</p>
              </div>
            </div>
            
            <div class="flex items-center gap-4">
              <div class="p-3 glass rounded-lg text-secondary border-white/5">
                <MapPin :size="24" />
              </div>
              <div>
                <p class="text-xs text-gray-500 uppercase font-bold tracking-widest">Lokasi</p>
                <p class="text-lg font-medium">Indonesia</p>
              </div>
            </div>
            
            <!-- <div class="flex items-center gap-4">
              <div class="p-3 glass rounded-lg text-accent border-white/5">
                <Phone :size="24" />
              </div>
              <div>
                <p class="text-xs text-gray-500 uppercase font-bold tracking-widest">Telepon</p>
                <p class="text-lg font-medium">+62 123 4567 890</p>
              </div>
            </div> -->
          </div>
        </div>

        <div class="contact-animate glass p-8 rounded-3xl border-white/5 relative overflow-hidden">
          <div class="absolute top-0 right-0 w-32 h-32 bg-primary/20 blur-[80px] -mr-16 -mt-16"></div>
          
          <form class="space-y-6 relative z-10" @submit.prevent="handleSubmit">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div class="space-y-2">
                <label class="text-sm font-medium text-gray-400">Nama Lengkap</label>
                <input 
                  v-model="form.name"
                  type="text" 
                  placeholder="Masukkan nama lengkap"
                  required
                  class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 focus:outline-none focus:border-primary/50 transition-colors"
                >
              </div>
              <div class="space-y-2">
                <label class="text-sm font-medium text-gray-400">Alamat Email</label>
                <input 
                  v-model="form.email"
                  type="email" 
                  placeholder="email@gmail.com"
                  required
                  class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 focus:outline-none focus:border-primary/50 transition-colors"
                >
              </div>
            </div>
            
            <div class="space-y-2">
              <label class="text-sm font-medium text-gray-400">Subjek</label>
              <input 
                v-model="form.subject"
                type="text" 
                placeholder="Pertanyaan Proyek"
                required
                class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 focus:outline-none focus:border-primary/50 transition-colors"
              >
            </div>
            
            <div class="space-y-2">
              <label class="text-sm font-medium text-gray-400">Pesan</label>
              <textarea 
                v-model="form.message"
                rows="5" 
                placeholder="Ceritakan tentang proyek Anda..."
                required
                class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 focus:outline-none focus:border-primary/50 transition-colors resize-none"
              ></textarea>
            </div>
            
            <button 
              type="submit"
              class="w-full py-4 bg-primary text-white rounded-xl font-bold flex items-center justify-center gap-2 hover:bg-primary/90 transition-all hover:scale-[1.02] active:scale-[0.98]"
            >
              Kirim Pesan <Send :size="18" />
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>
