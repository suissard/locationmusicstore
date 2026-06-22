<template>
  <section id="calculator" class="py-14 bg-dark-900">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
          <div class="grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
              
              <!-- Setup Inputs -->
              <div class="lg:col-span-7 bg-dark-800 border border-gray-800 p-5 sm:p-7 rounded-2xl space-y-6">
                  <div>
                      <h3 class="text-xl font-black text-white">1. Configurez votre événement</h3>
                      <p class="text-xs text-gray-400">Ajustez les options selon vos besoins réels.</p>
                  </div>

                  <!-- Config Display -->
                  <div class="p-3 bg-dark-950 rounded-xl border border-gray-850 flex items-center justify-between text-xs">
                      <div>
                          <span class="text-gray-500 block">Formule active :</span>
                          <span class="font-bold text-white">{{ selectedPackTitle }}</span>
                      </div>
                      <span class="text-xs text-brand-400 bg-brand-500/10 px-2.5 py-1 rounded-md font-bold">Base</span>
                  </div>

                  <!-- Addon switches -->
                  <div class="space-y-2">
                      <label class="flex items-center justify-between p-3.5 bg-dark-950 rounded-xl border border-gray-850 text-xs cursor-pointer select-none">
                          <span class="font-bold text-white">Micro Main sans fil Shure HF (+15€)</span>
                          <input type="checkbox" v-model="hasMicro" class="w-4 h-4 rounded border-gray-700 text-brand-600 focus:ring-brand-500 bg-dark-800">
                      </label>
                      <label class="flex items-center justify-between p-3.5 bg-dark-950 rounded-xl border border-gray-850 text-xs cursor-pointer select-none">
                          <span class="font-bold text-white">Option Livraison, Pose & Reprise (+60€)</span>
                          <input type="checkbox" v-model="hasDelivery" class="w-4 h-4 rounded border-gray-700 text-brand-600 focus:ring-brand-500 bg-dark-800">
                      </label>
                  </div>

                  <!-- Dynamic Basket items from Tab 2 -->
                  <div v-if="extrasList.length > 0" class="space-y-2">
                      <span class="text-xs font-bold text-gray-400 block">Matériels supplémentaires ajoutés :</span>
                      <div class="space-y-1.5">
                          <div v-for="(item, idx) in extrasList" :key="idx" class="flex items-center justify-between p-2 bg-dark-950 rounded-lg text-[11px] border border-gray-850">
                              <span class="text-gray-300">🎵 {{ item.name }}</span>
                              <div class="flex items-center gap-2">
                                  <span class="font-bold text-brand-400">+{{ item.price }}€</span>
                                  <button @click="$emit('removeExtraItem', idx)" type="button" class="text-neon-pink font-bold focus:outline-none">X</button>
                              </div>
                          </div>
                      </div>
                  </div>

                  <!-- Selector Zone -->
                  <div class="space-y-2">
                      <label class="text-xs font-bold text-gray-400 block" for="city-select">Lieu de l'événement :</label>
                      <select v-model="selectedCity" class="w-full bg-dark-950 border border-gray-800 rounded-xl p-3 text-white text-xs focus:outline-none focus:border-brand-500">
                          <option value="redon">Secteur Redon (Retrait gratuit au dépôt)</option>
                          <option value="rennes">Secteur Rennes / Ille-et-Vilaine</option>
                          <option value="nantes">Secteur Nantes / Loire-Atlantique</option>
                          <option value="labaule">Secteur La Baule / Presqu'île de Guérande</option>
                      </select>
                  </div>
              </div>

              <!-- Final Conversion Panel -->
              <div class="lg:col-span-5 bg-gradient-to-br from-brand-950/40 to-dark-950 border border-brand-500/20 p-5 sm:p-7 rounded-2xl space-y-6 shadow-xl">
                  <div class="text-center pb-4 border-b border-gray-800">
                      <span class="text-[10px] uppercase font-bold tracking-widest text-gray-400 block mb-1">Estimation weekend complet</span>
                      <span class="text-4xl font-black text-white">{{ totalPriceDisplay }}</span>
                      <span class="block text-[11px] text-gray-500 mt-1">Tarif transparent net, aucun frais masqué</span>
                  </div>

                  <!-- Immediate Action Form -->
                  <form @submit.prevent="handleSubmit" class="space-y-3">
                      <input type="text" placeholder="Votre Prénom & Nom" required class="w-full bg-dark-950 border border-gray-850 rounded-xl p-3.5 text-xs text-white focus:outline-none focus:border-brand-500">
                      <div class="grid grid-cols-2 gap-2">
                          <input type="email" placeholder="E-mail" required class="w-full bg-dark-950 border border-gray-850 rounded-xl p-3.5 text-xs text-white focus:outline-none focus:border-brand-500">
                          <input type="tel" placeholder="Téléphone" required class="w-full bg-dark-950 border border-gray-850 rounded-xl p-3.5 text-xs text-white focus:outline-none focus:border-brand-500">
                      </div>
                      <input type="date" required v-model="formDate" class="w-full bg-dark-950 border border-gray-850 rounded-xl p-3.5 text-xs text-white focus:outline-none focus:border-brand-500">
                      
                      <button type="submit" class="w-full bg-gradient-to-r from-brand-600 to-neon-pink text-white font-black uppercase text-xs py-4 rounded-xl shadow-lg flex items-center justify-center gap-2 border-b-4 border-purple-800 active:border-b-0 tracking-wider">
                          🚀 Réserver mes dates en priorité
                      </button>
                  </form>
              </div>

          </div>
      </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
  selectedPackTitle: { type: String, default: 'Pack Anniversaire' },
  basePrice: { type: Number, default: 99 },
  extrasList: { type: Array, default: () => [] },
  hasMicro: Boolean,
  hasDelivery: Boolean
});

const emit = defineEmits(['update:hasMicro', 'update:hasDelivery', 'removeExtraItem', 'submitForm']);

const hasMicro = computed({
  get: () => props.hasMicro,
  set: (val) => emit('update:hasMicro', val)
});

const hasDelivery = computed({
  get: () => props.hasDelivery,
  set: (val) => emit('update:hasDelivery', val)
});

const selectedCity = ref('redon');
const formDate = ref('');

const totalPriceDisplay = computed(() => {
  if (props.basePrice === 0) return "Sur Devis";
  let total = props.basePrice;
  if (hasMicro.value) total += 15;
  if (hasDelivery.value) total += 60;
  props.extrasList.forEach(item => total += item.price);
  return `${total}€`;
});

function handleSubmit() {
  const formatted = new Date(formDate.value).toLocaleDateString('fr-FR', {year: 'numeric', month: 'long', day: 'numeric'});
  emit('submitForm', formatted);
}
</script>
