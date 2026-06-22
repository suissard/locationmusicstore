<template>
  <div class="pointer-events-none absolute inset-0 z-0 overflow-hidden">
      <!-- Interactive Nightclub Lasers and Spots -->
      <div :class="['spotlight left-0', { active: isFlashing }]" :style="spotLeftStyle"></div>
      <div :class="['spotlight right-0', { active: isFlashing }]" :style="spotRightStyle" style="background: conic-gradient(from 180deg at 50% 0%, rgba(6, 182, 212, 0.4) 0deg, rgba(139, 92, 246, 0.4) 45deg, transparent 90deg, transparent 360deg);"></div>

      <!-- Laser lines backdrop -->
      <div class="absolute top-0 inset-x-0 h-[500px] overflow-hidden pointer-events-none z-0">
          <div class="absolute top-0 left-1/4 w-[1px] h-[800px] bg-gradient-to-b from-neon-pink to-transparent origin-top animate-laser-sweep-left"></div>
          <div class="absolute top-0 right-1/4 w-[1px] h-[800px] bg-gradient-to-b from-neon-cyan to-transparent origin-top animate-laser-sweep-right"></div>
      </div>

      <!-- Dynamic Beams container -->
      <div v-for="beam in dynamicBeams" :key="beam.id"
           class="spotlight-beam-dynamic"
           :style="beam.style">
      </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
  triggerFlash: Number,
  triggerDynamic: Number
});

const isFlashing = ref(false);
const spotLeftStyle = ref({});
const spotRightStyle = ref({});

watch(() => props.triggerFlash, () => {
  if (props.triggerFlash > 0) {
      isFlashing.value = true;
      spotLeftStyle.value = { transform: `scale(1.2) rotate(${Math.floor(Math.random() * 50) - 15}deg)` };
      spotRightStyle.value = { transform: `scale(1.2) rotate(${Math.floor(Math.random() * 50) - 35}deg)` };

      setTimeout(() => {
          isFlashing.value = false;
          spotLeftStyle.value = {};
          spotRightStyle.value = {};
      }, 800);
  }
});

const dynamicBeams = ref([]);
let beamId = 0;

watch(() => props.triggerDynamic, () => {
  if (props.triggerDynamic > 0) {
      const colors = ['#f43f5e', '#06b6d4', '#eab308', '#8b5cf6', '#10b981'];
      const numBeams = 3;

      for (let i = 0; i < numBeams; i++) {
          const originX = Math.random() * window.innerWidth;
          const originY = Math.random() * 60;
          const randomColor = colors[Math.floor(Math.random() * colors.length)];
          const startAngle = (Math.random() * 100 - 50);
          const targetAngle = startAngle + (Math.random() * 30 - 15);
          
          const id = beamId++;
          
          const newBeam = {
              id,
              style: {
                  left: `${originX}px`,
                  top: `${originY}px`,
                  width: '0px',
                  height: '0px',
                  borderLeft: '60px solid transparent',
                  borderRight: '60px solid transparent',
                  borderBottom: `${window.innerHeight * 1.5}px solid ${randomColor}70`,
                  transform: `rotate(${startAngle}deg) scale(0)`,
                  opacity: '0',
                  transition: 'opacity 1.2s ease-out, transform 1.2s ease-out'
              }
          };

          dynamicBeams.value.push(newBeam);

          setTimeout(() => {
              const beamRef = dynamicBeams.value.find(b => b.id === id);
              if(beamRef) {
                  beamRef.style.transform = `rotate(${targetAngle}deg) scale(1.2)`;
                  beamRef.style.opacity = '0.6';
              }
          }, 50);

          setTimeout(() => {
              const beamRef = dynamicBeams.value.find(b => b.id === id);
              if(beamRef) {
                  beamRef.style.opacity = '0';
                  beamRef.style.transform = `rotate(${targetAngle * 1.2}deg) scale(1.4)`;
              }
              setTimeout(() => {
                  dynamicBeams.value = dynamicBeams.value.filter(b => b.id !== id);
              }, 1200);
          }, 1050);
      }
  }
});
</script>
