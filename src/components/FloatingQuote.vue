<template>
  <div :class="[
      'fixed bottom-6 left-6 z-40 transition-all duration-500 transform',
      isVisible ? 'translate-y-0 opacity-100' : 'translate-y-20 opacity-0 pointer-events-none'
  ]">
      <button @click="scrollToQuote" class="group relative flex items-center gap-3 bg-neutral-900/90 backdrop-blur-md border border-brand-500/30 p-3 rounded-2xl shadow-[0_8px_30px_rgb(0,0,0,0.4)] hover:shadow-brand-500/20 hover:border-brand-500/60 transition-all duration-300">
          
          <!-- Icon -->
          <div class="relative w-10 h-10 rounded-xl bg-brand-500/20 text-brand-400 flex items-center justify-center border border-brand-500/30 group-hover:scale-105 transition-transform">
              <svg class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-3 7h3m-3 4h3m-6-4h.01M9 16h.01" />
              </svg>
              <!-- Badge -->
              <span class="absolute -top-2 -right-2 bg-neon-pink text-white text-[9px] font-bold px-1.5 py-0.5 rounded-full min-w-[18px] text-center shadow-lg">
                  {{ itemCount }}
              </span>
          </div>

          <!-- Text -->
          <div class="text-left pr-2">
              <span class="block text-[10px] uppercase tracking-widest text-brand-400 font-bold mb-0.5">Mon Devis</span>
              <span class="block text-sm font-black text-white">{{ total }}</span>
          </div>

          <!-- Arrow -->
          <div class="absolute right-3 opacity-0 -translate-x-2 group-hover:opacity-100 group-hover:translate-x-0 transition-all text-brand-400">
              <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
          </div>
      </button>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, watch } from 'vue';

const props = defineProps({
  itemCount: {
      type: Number,
      default: 0
  },
  total: {
      type: String,
      default: '0€'
  }
});

const isVisible = ref(false);

function scrollToQuote() {
  const el = document.getElementById('calculator');
  if (el) el.scrollIntoView({ behavior: 'smooth' });
}

onMounted(() => {
  window.addEventListener('scroll', updateVisibility, { passive: true });
  updateVisibility();
});

onUnmounted(() => {
  window.removeEventListener('scroll', updateVisibility);
});

function updateVisibility() {
  const el = document.getElementById('calculator');
  if (el) {
      const rect = el.getBoundingClientRect();
      // It's visible if top is less than window height and bottom is greater than 0
      const isVisibleNow = (rect.top < window.innerHeight && rect.bottom > 0);
      
      // Only show if we have items AND calculator is NOT in view
      isVisible.value = props.itemCount > 0 && !isVisibleNow;
  } else {
      isVisible.value = props.itemCount > 0;
  }
}

watch(() => props.itemCount, () => {
  updateVisibility();
});
</script>
