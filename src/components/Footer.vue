<script setup>
import { Rocket } from 'lucide-vue-next'
</script>

<template>
  <footer class="py-12 border-t border-white/5 bg-dark">
    <div class="max-w-7xl mx-auto px-6">
      <div class="flex flex-col md:flex-row justify-between items-center gap-8 mb-12">
        <div class="flex items-center space-x-2 font-mono font-bold text-xl">
          <Rocket class="text-primary" :size="24" />
          <span class="bg-gradient-to-r from-primary to-secondary bg-clip-text text-transparent">
            YUSUF.DEV
          </span>
        </div>
        
        <div class="flex gap-8 text-sm text-gray-400">
          <a href="#" class="hover:text-primary transition-colors">Kebijakan Privasi</a>
          <a href="#" class="hover:text-primary transition-colors">Syarat Layanan</a>
          <a href="#" class="hover:text-primary transition-colors">Cookie</a>
        </div>
        
        <div class="text-sm text-gray-500">
          &copy; 2026 Portofolio Yusuf Saputra.
        </div>
      </div>
    </div>
  </footer>
</template>
