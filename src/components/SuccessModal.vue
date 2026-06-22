<template>
  <div v-if="isOpen" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-dark-950/90 backdrop-blur-md">
      <div class="bg-dark-800 border border-brand-500/40 p-6 rounded-2xl max-w-sm w-full text-center space-y-4">
          <div class="w-12 h-12 bg-emerald-500/10 text-emerald-400 rounded-full flex items-center justify-center mx-auto text-xl font-bold">✓</div>
          <h3 class="text-xl font-black text-white">Demande validée !</h3>
          <p class="text-xs text-gray-400 leading-relaxed">Notre équipe vérifie le stock disponible pour le <span class="text-brand-400 font-bold">{{ dateStr }}</span>. Votre devis final gratuit vous attend sur votre mail sous 2h max. ⚡</p>
          <button @click="$emit('close')" class="w-full bg-brand-600 text-white font-bold py-2.5 rounded-xl text-xs uppercase tracking-wider">Parfait, merci !</button>
      </div>
  </div>
</template>

<script setup>
defineProps({
  isOpen: Boolean,
  dateStr: String
});
defineEmits(['close']);
</script>
