<template>
  <div class="relative w-full h-full">
      <BackgroundEffects :triggerFlash="flashTrigger" :triggerDynamic="dynamicTrigger" />
      
      <HeaderNav @trigger-lights="handleHeaderClick" />
      
      <main>
          <HeroSection @trigger-lights="handleHeaderClick" />
          
          <OffersSection 
              @selectPack="handleSelectPack" 
              @addItem="handleAddItem" 
              ref="offersRef"
          />
          
          <CalculatorSection 
              ref="calculatorRef"
              :selectedPackTitle="selectedPackTitle"
              :basePrice="basePrice"
              :extrasList="extrasList"
              v-model:hasMicro="hasMicro"
              v-model:hasDelivery="hasDelivery"
              @removeExtraItem="removeExtraItem"
              @submitForm="handleFormSubmit"
          />
      </main>

      <FooterSection />

      <SuccessModal 
          :isOpen="isModalOpen"
          :dateStr="modalDate"
          @close="closeModal"
      />
  </div>
</template>

<script setup>
import { ref, nextTick } from 'vue';
import HeaderNav from './components/HeaderNav.vue';
import HeroSection from './components/HeroSection.vue';
import OffersSection from './components/OffersSection.vue';
import CalculatorSection from './components/CalculatorSection.vue';
import FooterSection from './components/FooterSection.vue';
import BackgroundEffects from './components/BackgroundEffects.vue';
import SuccessModal from './components/SuccessModal.vue';

const flashTrigger = ref(0);
const dynamicTrigger = ref(0);
const calculatorRef = ref(null);

const basePrice = ref(99);
const selectedPackTitle = ref('Pack Anniversaire');
const extrasList = ref([]);
const hasMicro = ref(false);
const hasDelivery = ref(false);

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
