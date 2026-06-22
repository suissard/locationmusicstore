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
                  <div class="p-4 bg-dark-950 rounded-xl border border-gray-850 flex flex-col gap-3 text-xs">
                      <div class="flex flex-col gap-2">
                          <span class="font-bold text-white mb-1">Formule choisie :</span>
                          <select v-model="internalPackSelect" class="w-full bg-dark-900 border border-gray-800 rounded-xl p-3 text-white text-xs focus:outline-none focus:border-brand-500">
                              <option value="none">Aucun pack (Matériel à la carte)</option>
                              <option v-for="pack in availablePacks" :key="pack.name" :value="pack.name">{{ pack.name }} ({{ pack.price }}€)</option>
                              <option v-if="isCustomPack" :value="selectedPackTitle">{{ selectedPackTitle }} ({{ basePrice }}€)</option>
                          </select>
                      </div>
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
                  <div class="space-y-3">
                      <span class="text-xs font-bold text-gray-400 block">Matériels supplémentaires :</span>
                      
                      <div v-if="groupedExtras.length > 0" class="space-y-2 mb-4">
                          <div v-for="group in groupedExtras" :key="group.name" class="flex items-center justify-between p-2.5 bg-dark-950 rounded-xl border border-gray-800 shadow-sm">
                              <div class="flex items-center gap-2.5">
                                  <span class="flex items-center justify-center w-7 h-7 rounded-lg bg-neon-pink text-white font-black text-[13px] shadow-[0_0_10px_rgba(236,72,153,0.3)]">{{ group.count }}x</span>
                                  <span class="text-gray-200 font-bold text-xs">{{ group.name }}</span>
                              </div>
                              <div class="flex items-center gap-3">
                                  <span class="font-bold text-brand-400 text-xs">+{{ group.totalPrice }}€</span>
                                  <button @click="$emit('removeExtraItem', group.firstIdx)" type="button" class="w-7 h-7 flex items-center justify-center rounded-lg bg-red-500/10 text-red-400 border border-red-500/20 hover:bg-red-500 hover:text-white transition-all cursor-pointer">
                                      <svg class="w-3.5 h-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M6 18L18 6M6 6l12 12" /></svg>
                                  </button>
                              </div>
                          </div>
                      </div>

                      <select v-model="selectedNewExtra" @change="addSelectedExtra" class="w-full bg-dark-950 border border-gray-800 rounded-xl p-3 text-white text-xs focus:outline-none focus:border-brand-500">
                          <option value="">+ Ajouter du matériel...</option>
                          <optgroup label="Enceintes Individuelles">
                              <option v-for="item in availableEnceintes" :key="item.name" :value="item">{{ item.name }} (+{{ item.price }}€)</option>
                          </optgroup>
                          <optgroup label="Suppléments & Options">
                              <option v-for="item in availableSupplements" :key="item.name" :value="item">{{ item.name }} (+{{ item.price }}€)</option>
                          </optgroup>
                      </select>
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
import equipmentData from '../data/equipment.json';

const props = defineProps({
  isPackActive: { type: Boolean, default: false },
  selectedPackTitle: { type: String, default: 'Pack Anniversaire' },
  basePrice: { type: Number, default: 99 },
  extrasList: { type: Array, default: () => [] },
  hasMicro: Boolean,
  hasDelivery: Boolean
});

const emit = defineEmits(['update:isPackActive', 'update:selectedPackTitle', 'update:basePrice', 'update:hasMicro', 'update:hasDelivery', 'removeExtraItem', 'addExtraItem', 'submitForm']);

const isPackActive = computed({
  get: () => props.isPackActive,
  set: (val) => emit('update:isPackActive', val)
});

const availablePacks = equipmentData.packs_anniversaire;

const isCustomPack = computed(() => {
  return props.selectedPackTitle && !availablePacks.find(p => p.name === props.selectedPackTitle);
});

const internalPackSelect = computed({
  get: () => props.isPackActive ? props.selectedPackTitle : 'none',
  set: (val) => {
     if (val === 'none') {
         emit('update:isPackActive', false);
     } else {
         emit('update:isPackActive', true);
         const pack = availablePacks.find(p => p.name === val);
         if (pack) {
             emit('update:selectedPackTitle', pack.name);
             emit('update:basePrice', pack.price);
         }
     }
  }
});

const hasMicro = computed({
  get: () => props.hasMicro,
  set: (val) => emit('update:hasMicro', val)
});

const hasDelivery = computed({
  get: () => props.hasDelivery,
  set: (val) => emit('update:hasDelivery', val)
});

const availableEnceintes = equipmentData.enceintes_individuelles;
const availableSupplements = equipmentData.supplements;
const selectedNewExtra = ref("");

function addSelectedExtra() {
    if (selectedNewExtra.value && selectedNewExtra.value.name) {
        emit('addExtraItem', { name: selectedNewExtra.value.name, price: selectedNewExtra.value.price });
        selectedNewExtra.value = "";
    }
}

const groupedExtras = computed(() => {
    const groups = {};
    props.extrasList.forEach((item, idx) => {
        if (!groups[item.name]) {
            groups[item.name] = { name: item.name, price: item.price, count: 0, totalPrice: 0, firstIdx: idx };
        }
        groups[item.name].count++;
        groups[item.name].totalPrice += item.price;
        // Keep the largest index as firstIdx so removing removes the latest one added
        groups[item.name].firstIdx = idx;
    });
    return Object.values(groups);
});

const selectedCity = ref('redon');
const formDate = ref('');

const totalPriceDisplay = computed(() => {
  if (!isPackActive.value && props.extrasList.length === 0) return "Sur Devis";
  
  let total = 0;
  if (isPackActive.value) total += props.basePrice;
  if (hasMicro.value) total += 15;
  if (hasDelivery.value) total += 60;
  props.extrasList.forEach(item => total += item.price);
  
  return total > 0 ? `${total}€` : "Sur Devis";
});

function handleSubmit() {
  const formatted = new Date(formDate.value).toLocaleDateString('fr-FR', {year: 'numeric', month: 'long', day: 'numeric'});
  emit('submitForm', formatted);
}
</script>
