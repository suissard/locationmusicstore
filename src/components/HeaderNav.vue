<template>
  <header class="sticky top-0 z-50 bg-dark-950/90 backdrop-blur-md border-b border-gray-800/80">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
          <!-- Brand Logo -->
          <a href="#" class="flex items-center space-x-2.5">
              <div class="p-2 bg-gradient-to-tr from-brand-600 to-neon-pink rounded-xl text-white shadow-lg">
                  <svg class="w-5.5 h-5.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M9 18V5l12-2v13"></path><circle cx="6" cy="18" r="3"></circle><circle cx="18" cy="16" r="3"></circle></svg>
              </div>
              <div class="leading-none">
                  <span class="text-base sm:text-lg font-black tracking-wider text-white">LOCATION<span class="text-brand-500">MUSIC</span>STORE</span>
                  <span class="block text-[9px] text-gray-400 font-bold tracking-widest uppercase">Son & Lumières Pro</span>
              </div>
          </a>

          <!-- CTA Actions -->
          <div class="flex items-center space-x-3">
              <a href="tel:0658793867" class="hidden sm:flex items-center text-xs font-bold text-gray-300 bg-dark-900 border border-gray-800 px-3.5 py-2 rounded-xl hover:text-white">
                  <svg class="w-3.5 h-3.5 mr-2 text-brand-500" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path></svg>
                  06 58 79 38 67
              </a>
              <button @click="$emit('trigger-lights', 'calculator')" class="bg-gradient-to-r from-brand-600 to-neon-pink text-white text-xs font-black uppercase tracking-widest px-4 py-2.5 sm:px-5 sm:py-3.5 rounded-xl transition-all shadow-lg hover:shadow-brand-500/20 active:scale-95 flex items-center gap-1.5 border-b-2 border-brand-700">
                  <svg class="w-3.5 h-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M12 2v20M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"></path></svg> Louer Maintenant
              </button>
          </div>
      </div>
  </header>
</template>

<script setup>
</script>
