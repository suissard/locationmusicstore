<template>
  <div class="relative w-full h-full">
      <BackgroundEffects :triggerFlash="flashTrigger" :triggerDynamic="dynamicTrigger" />
      
      <HeaderNav @trigger-lights="handleHeaderClick" />
      
      <main>
          <HeroSection @trigger-lights="handleHeaderClick" />
          
          <OffersSection 
              @selectPack="handleSelectPack" 
              @addItem="handleAddItem" 
              @removeItemByName="handleRemoveItemByName"
              :extrasList="extrasList"
              ref="offersRef"
          />
          
          <CalculatorSection 
              ref="calculatorRef"
              v-model:isPackActive="isPackActive"
              v-model:selectedPackTitle="selectedPackTitle"
              v-model:basePrice="basePrice"
              :extrasList="extrasList"
              v-model:hasMicro="hasMicro"
              v-model:hasDelivery="hasDelivery"
              @removeExtraItem="removeExtraItem"
              @addExtraItem="handleAddItem"
              @submitForm="handleFormSubmit"
          />
      </main>

      <FooterSection />

      <SuccessModal 
          :isOpen="isModalOpen"
          :dateStr="modalDate"
          @close="closeModal"
      />

      <FloatingChat />
      <FloatingQuote :itemCount="quoteItemCount" :total="quoteTotal" />
  </div>
</template>

<script setup>
import { ref, nextTick, computed } from 'vue';
import HeaderNav from './components/HeaderNav.vue';
import HeroSection from './components/HeroSection.vue';
import OffersSection from './components/OffersSection.vue';
import CalculatorSection from './components/CalculatorSection.vue';
import FooterSection from './components/FooterSection.vue';
import BackgroundEffects from './components/BackgroundEffects.vue';
import SuccessModal from './components/SuccessModal.vue';
import FloatingChat from './components/FloatingChat.vue';
import FloatingQuote from './components/FloatingQuote.vue';
import equipmentData from './data/equipment.json';

const flashTrigger = ref(0);
const dynamicTrigger = ref(0);
const calculatorRef = ref(null);

const isPackActive = ref(false);
const basePrice = ref(equipmentData.packs_anniversaire[0].price);
const selectedPackTitle = ref(equipmentData.packs_anniversaire[0].name);
const extrasList = ref([]);
const hasMicro = ref(false);
const hasDelivery = ref(false);

const quoteItemCount = computed(() => {
  let count = 0;
  if (isPackActive.value) count += 1;
  if (hasMicro.value) count += 1;
  if (hasDelivery.value) count += 1;
  count += extrasList.value.length;
  return count;
});

const quoteTotal = computed(() => {
  if (basePrice.value === 0 && !isPackActive.value && extrasList.value.length === 0 && !hasMicro.value && !hasDelivery.value) return "0€";
  
  let total = isPackActive.value ? basePrice.value : 0;
  if (hasMicro.value) total += 15;
  if (hasDelivery.value) total += 60;
  extrasList.value.forEach(item => total += item.price);
  return total > 0 ? `${total}€` : "Sur Devis";
});

const isModalOpen = ref(false);
const modalDate = ref('');

function handleHeaderClick(targetId) {
  flashTrigger.value++;
  setTimeout(() => {
      const el = document.getElementById(targetId);
      if (el) el.scrollIntoView({ behavior: 'smooth' });
  }, 100);
}

function handleSelectPack({ type, price, title }) {
  dynamicTrigger.value++;
  isPackActive.value = true;
  basePrice.value = price;
  selectedPackTitle.value = title;
  
  setTimeout(() => {
      const el = document.getElementById('calculator');
      if (el) el.scrollIntoView({ behavior: 'smooth' });
  }, 100);
}

function handleAddItem({ name, price }) {
  dynamicTrigger.value++;
  extrasList.value.push({ name, price });
}

function removeExtraItem(idx) {
  extrasList.value.splice(idx, 1);
}

function handleRemoveItemByName(name) {
  const idx = extrasList.value.findIndex(item => item.name === name);
  if (idx !== -1) {
    extrasList.value.splice(idx, 1);
  }
}

function handleFormSubmit(dateStr) {
  modalDate.value = dateStr;
  isModalOpen.value = true;
}

function closeModal() {
  isModalOpen.value = false;
  hasMicro.value = false;
  hasDelivery.value = false;
  extrasList.value = [];
}
</script>

<style scoped>
/* Optional specific overrides */
</style>
