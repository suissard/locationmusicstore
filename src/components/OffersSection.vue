<template>
  <section id="offres" class="py-16 bg-dark-800 border-b border-gray-850 relative" style="font-family: 'Plus Jakarta Sans', sans-serif;">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
          
          <div class="text-center max-w-2xl mx-auto space-y-3 mb-12">
              <span class="text-xs font-bold text-neon-pink uppercase tracking-widest block">Nos Formules de Location</span>
              <h2 class="text-2xl sm:text-4xl font-extrabold text-white tracking-tight">Simple, modulable & sans stress</h2>
              <p class="text-xs sm:text-sm text-gray-400">Sélectionnez un pack tout-inclus ou accédez au catalogue pour composer à l'unité.</p>
              
              <!-- Tab controller buttons -->
              <div class="inline-flex p-1 bg-dark-950 rounded-2xl border border-gray-850 mt-6 w-full max-w-sm sm:max-w-md">
                  <button @click="activeTab = 'packs'" :class="[
                      'flex-1 text-center py-2.5 rounded-xl font-black text-xs uppercase tracking-wider transition-all shadow cursor-pointer',
                      activeTab === 'packs' ? 'bg-brand-600 text-white' : 'text-gray-400 hover:text-white'
                  ]">
                      🎉 Packs Tout-Inclus
                  </button>
                  <button @click="activeTab = 'catalogue'" :class="[
                      'flex-1 text-center py-2.5 rounded-xl font-black text-xs uppercase tracking-wider transition-all cursor-pointer',
                      activeTab === 'catalogue' ? 'bg-brand-600 text-white' : 'text-gray-400 hover:text-white'
                  ]">
                      🎛&nbsp;Matériel au Détail
                  </button>
              </div>
          </div>

          <!-- TAB 1: Packs list -->
          <div v-show="activeTab === 'packs'" class="parallax-perspective grid grid-cols-1 md:grid-cols-2 gap-8 w-full max-w-4xl mx-auto z-20 my-auto">
              
              <!-- ================= CARD 1 : MARIAGE (TEMPÊTE DE RIZ PAR VAGUES) ================= -->
              <div ref="weddingCard" id="weddingCard" class="relative group rounded-2xl border border-amber-500/15 bg-neutral-900/90 backdrop-blur-md overflow-hidden gold-glow transition-all duration-500 hover:border-amber-400/40 flex flex-col justify-between animate-float-gold">
                  
                  <!-- Canvas local confiné -->
                  <canvas ref="weddingCanvas" id="weddingCanvas" class="absolute inset-0 pointer-events-none z-10 rounded-2xl"></canvas>

                  <!-- Alliances en arrière-plan -->
                  <div class="absolute inset-0 flex items-center justify-center pointer-events-none z-0 overflow-hidden">
                      <svg class="w-[240px] h-[240px] animate-rings opacity-10" viewBox="0 0 200 120" xmlns="http://www.w3.org/2000/svg">
                          <defs>
                              <linearGradient id="goldGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                                  <stop offset="0%" stop-color="#8a5a16" />
                                  <stop offset="50%" stop-color="#d4af37" />
                                  <stop offset="100%" stop-color="#a67c1e" />
                              </linearGradient>
                          </defs>
                          <g>
                              <circle cx="75" cy="60" r="42" fill="none" stroke="url(#goldGrad)" stroke-width="8" />
                              <circle cx="125" cy="60" r="45" fill="none" stroke="url(#goldGrad)" stroke-width="10" />
                              <path d="M 103 27 A 45 45 0 0 1 147 27" fill="none" stroke="url(#goldGrad)" stroke-width="10" stroke-linecap="round" />
                          </g>
                      </svg>
                  </div>

                  <!-- Contenu -->
                  <div class="relative z-20 pt-12 pb-5 px-6 space-y-4">
                      <!-- Badge -->
                      <div class="absolute top-4 right-4 bg-gradient-to-r from-amber-500 to-yellow-600 text-black font-bold text-[9px] uppercase tracking-widest px-2.5 py-0.5 rounded-full z-10 animate-pulse">
                          💍 Union Chic
                      </div>

                      <div class="text-center space-y-2">
                          <h2 class="text-xl font-bold tracking-wide gold-shimmer" style="font-family: 'Cinzel Decorative', serif; line-height: 1.4;">
                              Pack "Fiançailles & Union"
                          </h2>
                          <p class="text-neutral-400 text-[11px] max-w-xs mx-auto">
                              Acoustique d'exception et lumières tamisées pour votre cocktail ou dîner de mariage.
                          </p>
                      </div>

                      <!-- Caractéristiques réduites -->
                      <div class="bg-black/30 border border-neutral-800/60 rounded-xl p-3 text-[11px] text-neutral-300">
                          <div class="grid grid-cols-2 gap-1.5">
                              <div><span class="text-amber-500">✔</span> 2x Enceintes Tri-amp</div>
                              <div><span class="text-amber-500">✔</span> 1x Caisson de Basse</div>
                              <div><span class="text-amber-500">✔</span> 2x Micros Sans-fil</div>
                              <div><span class="text-amber-500">✔</span> Pack Lumières LED</div>
                          </div>
                      </div>

                      <!-- Options -->
                      <div class="grid grid-cols-2 gap-2">
                          <button 
                              type="button"
                              @click="toggleWeddingOption('lights', $event)" 
                              :class="[
                                  'flex flex-col items-center justify-center p-2 rounded-xl border transition-all duration-300 cursor-pointer',
                                  weddingOptions.lights ? 'border-amber-400 bg-amber-950/20' : 'border-neutral-800 bg-neutral-950/50 hover:border-amber-500/40'
                              ]"
                          >
                              <span class="text-xs font-medium text-neutral-300">Option Lumières (+90€)</span>
                              <span :class="['text-[9px]', weddingOptions.lights ? 'text-amber-400 font-bold' : 'text-neutral-500']">
                                  {{ weddingOptions.lights ? 'Sélectionné ✓' : 'Non inclus' }}
                              </span>
                          </button>
                          <button 
                              type="button"
                              @click="toggleWeddingOption('smoke', $event)" 
                              :class="[
                                  'flex flex-col items-center justify-center p-2 rounded-xl border transition-all duration-300 cursor-pointer',
                                  weddingOptions.smoke ? 'border-amber-400 bg-amber-950/20' : 'border-neutral-800 bg-neutral-950/50 hover:border-amber-500/40'
                              ]"
                          >
                              <span class="text-xs font-medium text-neutral-300">Option Fumée (+120€)</span>
                              <span :class="['text-[9px]', weddingOptions.smoke ? 'text-amber-400 font-bold' : 'text-neutral-500']">
                                  {{ weddingOptions.smoke ? 'Sélectionné ✓' : 'Non inclus' }}
                              </span>
                          </button>
                      </div>
                  </div>

                  <!-- Footer -->
                  <div class="p-4 border-t border-neutral-800/80 bg-black/20 relative z-20">
                      <div class="flex items-center justify-between gap-3">
                          <div>
                              <p class="text-[9px] text-neutral-400 uppercase tracking-widest">Week-end</p>
                              <div class="flex items-baseline gap-0.5">
                                  <span class="text-2xl font-bold font-serif text-white">{{ displayedWeddingPrice }}</span>
                                  <span class="text-xs font-bold text-amber-400">€</span>
                              </div>
                          </div>
                          <button @click="triggerWeddingPurchase($event)" class="relative group overflow-hidden rounded-full py-2 px-5 gold-bg-shimmer font-bold text-neutral-950 shadow-md transition-all duration-300 transform active:scale-95 text-[11px] uppercase tracking-wider cursor-pointer">
                              <span class="relative flex items-center gap-1">
                                  <span>{{ weddingBtnText }}</span>
                                  <span>🌾</span>
                              </span>
                          </button>
                      </div>
                  </div>
              </div>

              <!-- ================= CARD 2 : ANNIVERSAIRE (BALLONS & BULLES) ================= -->
              <div ref="birthdayCard" id="birthdayCard" class="relative group rounded-2xl border border-pink-500/15 bg-neutral-950/90 backdrop-blur-md overflow-hidden neon-glow transition-all duration-500 hover:border-pink-400/40 flex flex-col justify-between animate-float-neon">
                  
                  <!-- Canvas local confiné -->
                  <canvas ref="birthdayCanvas" id="birthdayCanvas" class="absolute inset-0 pointer-events-none z-10 rounded-2xl"></canvas>

                  <!-- Étoiles en arrière-plan -->
                  <div class="absolute inset-0 flex items-center justify-center pointer-events-none z-0 overflow-hidden">
                      <svg class="w-[240px] h-[240px] animate-stars opacity-8" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
                          <defs>
                              <linearGradient id="neonGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                                  <stop offset="0%" stop-color="#ec4899" />
                                  <stop offset="100%" stop-color="#3b82f6" />
                              </linearGradient>
                          </defs>
                          <g>
                              <path d="M 100 20 L 118 70 L 170 70 L 128 102 L 145 152 L 100 122 L 55 152 L 72 102 L 30 70 L 82 70 Z" fill="none" stroke="url(#neonGrad)" stroke-width="2" />
                          </g>
                      </svg>
                  </div>

                  <!-- Contenu -->
                  <div class="relative z-20 pt-12 pb-5 px-6 space-y-4">
                      <!-- Badge -->
                      <div class="absolute top-4 right-4 bg-gradient-to-r from-pink-500 to-purple-600 text-white font-bold text-[9px] uppercase tracking-widest px-2.5 py-0.5 rounded-full z-10 animate-pulse">
                          🎂 VIP Party
                      </div>

                      <div class="text-center space-y-2">
                          <h2 class="text-xl font-bold tracking-wide neon-shimmer" style="font-family: 'Righteous', sans-serif; line-height: 1.4;">
                              Pack "Anniversaire VIP"
                          </h2>
                          <p class="text-neutral-400 text-[11px] max-w-xs mx-auto">
                              Des basses explosives et une ambiance festive dynamique pour danser toute la nuit.
                          </p>
                      </div>

                      <!-- Caractéristiques réduites -->
                      <div class="bg-purple-950/10 border border-purple-500/10 rounded-xl p-3 text-[11px] text-neutral-300">
                          <div class="grid grid-cols-2 gap-1.5">
                              <div><span class="text-pink-500">⚡</span> 2x Enceintes Active</div>
                              <div><span class="text-pink-500">⚡</span> 1x Jeu de lumière LED</div>
                              <div><span class="text-pink-500">⚡</span> 1x Micro filaire HF</div>
                              <div><span class="text-pink-500">⚡</span> Bluetooth & Playlist</div>
                          </div>
                      </div>

                      <!-- Options -->
                      <div class="grid grid-cols-2 gap-2">
                          <button 
                              type="button"
                              @click="toggleBirthdayOption('confetti', $event)" 
                              :class="[
                                  'flex flex-col items-center justify-center p-2 rounded-xl border transition-all duration-300 cursor-pointer',
                                  birthdayOptions.confetti ? 'border-pink-400 bg-pink-950/20' : 'border-neutral-800 bg-neutral-950/50 hover:border-pink-500/40'
                              ]"
                          >
                              <span class="text-xs font-medium text-neutral-300">Confettis (+40€)</span>
                              <span :class="['text-[9px]', birthdayOptions.confetti ? 'text-pink-400 font-bold' : 'text-neutral-500']">
                                  {{ birthdayOptions.confetti ? 'Sélectionné ✓' : 'Non inclus' }}
                              </span>
                          </button>
                          <button 
                              type="button"
                              @click="toggleBirthdayOption('bubbles', $event)" 
                              :class="[
                                  'flex flex-col items-center justify-center p-2 rounded-xl border transition-all duration-300 cursor-pointer',
                                  birthdayOptions.bubbles ? 'border-pink-400 bg-pink-950/20' : 'border-neutral-800 bg-neutral-950/50 hover:border-pink-500/40'
                              ]"
                          >
                              <span class="text-xs font-medium text-neutral-300">Mach. Bulles (+50€)</span>
                              <span :class="['text-[9px]', birthdayOptions.bubbles ? 'text-pink-400 font-bold' : 'text-neutral-500']">
                                  {{ birthdayOptions.bubbles ? 'Sélectionné ✓' : 'Non inclus' }}
                              </span>
                          </button>
                      </div>
                  </div>

                  <!-- Footer -->
                  <div class="p-4 border-t border-neutral-800/80 bg-black/20 relative z-20">
                      <div class="flex items-center justify-between gap-3">
                          <div>
                              <p class="text-[9px] text-neutral-400 uppercase tracking-widest">Week-end</p>
                              <div class="flex items-baseline gap-0.5">
                                  <span class="text-2xl font-bold font-serif text-white">{{ displayedBirthdayPrice }}</span>
                                  <span class="text-xs font-bold text-pink-400">€</span>
                              </div>
                          </div>
                          <button @click="triggerBirthdayPurchase($event)" class="relative group overflow-hidden rounded-full py-2 px-5 neon-bg-shimmer font-bold text-white shadow-md transition-all duration-300 transform active:scale-95 text-[11px] uppercase tracking-wider cursor-pointer">
                              <span class="relative flex items-center gap-1">
                                  <span>{{ birthdayBtnText }}</span>
                                  <span>🎈</span>
                              </span>
                          </button>
                      </div>
                  </div>
              </div>

          </div>

          <!-- TAB 2: Catalogue detail -->
          <div v-show="activeTab === 'catalogue'" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
              <!-- Item 1 -->
              <div class="bg-dark-900 border border-gray-800 rounded-xl p-4 flex flex-col justify-between">
                  <div class="space-y-2">
                      <div class="h-28 rounded-lg bg-dark-950 flex items-center justify-center text-gray-700 border border-gray-850">
                          <svg class="w-10 h-10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="5" y="2" width="14" height="20" rx="2"></rect><circle cx="12" cy="7" r="2"></circle><circle cx="12" cy="15" r="3"></circle></svg>
                      </div>
                      <h4 class="text-xs font-bold text-white uppercase tracking-wider">Enceinte active supplémentaire (500W)</h4>
                      <p class="text-[11px] text-gray-400">Pour diffuser du son dans une deuxième pièce adjacente ou le cocktail.</p>
                  </div>
                  <div class="pt-3 mt-3 border-t border-gray-800 flex items-center justify-between text-xs">
                      <span class="font-bold text-white">35€ <span class="text-gray-500 font-normal">/ we</span></span>
                      <button @click="addItem('Enceinte active supp.', 35)" class="px-2.5 py-1.5 bg-brand-600/20 text-brand-300 font-bold rounded-lg border border-brand-500/20 hover:bg-brand-600 hover:text-white transition-all text-[10px] cursor-pointer">
                          + Ajouter au devis
                      </button>
                  </div>
              </div>

              <!-- Item 2 -->
              <div class="bg-dark-900 border border-gray-800 rounded-xl p-4 flex flex-col justify-between">
                  <div class="space-y-2">
                      <div class="h-28 rounded-lg bg-dark-950 flex items-center justify-center text-gray-700 border border-gray-850">
                          <svg class="w-10 h-10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><circle cx="12" cy="12" r="10"></circle><path d="m15 9-6 6M9 9h6v6"></path></svg>
                      </div>
                      <h4 class="text-xs font-bold text-white uppercase tracking-wider">Projecteur d'ambiance LED coloré</h4>
                      <p class="text-[11px] text-gray-400">Créez une atmosphère de couleur fixe ou changeante contre les murs.</p>
                  </div>
                  <div class="pt-3 mt-3 border-t border-gray-800 flex items-center justify-between text-xs">
                      <span class="font-bold text-white">15€ <span class="text-gray-500 font-normal">/ we</span></span>
                      <button @click="addItem('Projecteur LED d\'ambiance', 15)" class="px-2.5 py-1.5 bg-brand-600/20 text-brand-300 font-bold rounded-lg border border-brand-500/20 hover:bg-brand-600 hover:text-white transition-all text-[10px] cursor-pointer">
                          + Ajouter au devis
                      </button>
                  </div>
              </div>

              <!-- Item 3 -->
              <div class="bg-dark-900 border border-gray-800 rounded-xl p-4 flex flex-col justify-between">
                  <div class="space-y-2">
                      <div class="h-28 rounded-lg bg-dark-950 flex items-center justify-center text-gray-700 border border-gray-850">
                          <svg class="w-10 h-10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M12 2v20M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"></path></svg>
                      </div>
                      <h4 class="text-xs font-bold text-white uppercase tracking-wider">Machine à fumée lourde</h4>
                      <p class="text-[11px] text-gray-400">Pour créer un tapis de nuage blanc au sol, effet féérique garanti.</p>
                  </div>
                  <div class="pt-3 mt-3 border-t border-gray-800 flex items-center justify-between text-xs">
                      <span class="font-bold text-white">49€ <span class="text-gray-500 font-normal">/ we</span></span>
                      <button @click="addItem('Machine à fumée lourde', 49)" class="px-2.5 py-1.5 bg-brand-600/20 text-brand-300 font-bold rounded-lg border border-brand-500/20 hover:bg-brand-600 hover:text-white transition-all text-[10px] cursor-pointer">
                          + Ajouter au devis
                      </button>
                  </div>
              </div>
          </div>

      </div>
  </section>

  <!-- Notification de réussite -->
  <div :class="[
      'fixed bottom-6 right-6 bg-neutral-900/95 border text-white px-5 py-3 rounded-xl shadow-2xl transition-all duration-500 flex items-center gap-3 z-50 max-w-sm',
      toastOpen ? 'translate-y-0 opacity-100' : 'translate-y-20 opacity-0 pointer-events-none',
      toastIsWedding ? 'border-amber-500/50' : 'border-pink-500/50'
  ]">
      <span class="text-xl">{{ toastEmoji }}</span>
      <div>
          <p class="font-bold text-xs">{{ toastTitle }}</p>
          <p class="text-[10px] text-neutral-300">{{ toastDesc }}</p>
      </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed, watch, nextTick } from 'vue';

const emit = defineEmits(['selectPack', 'addItem']);
const activeTab = ref('packs');

// Template refs
const weddingCard = ref(null);
const weddingCanvas = ref(null);
const birthdayCard = ref(null);
const birthdayCanvas = ref(null);

// Card Option States
const weddingOptions = ref({ lights: false, smoke: false });
const birthdayOptions = ref({ confetti: false, bubbles: false });

const weddingPrice = computed(() => {
  let total = 690;
  if (weddingOptions.value.lights) total += 90;
  if (weddingOptions.value.smoke) total += 120;
  return total;
});

const birthdayPrice = computed(() => {
  let total = 390;
  if (birthdayOptions.value.confetti) total += 40;
  if (birthdayOptions.value.bubbles) total += 50;
  return total;
});

// Price Animators
const displayedWeddingPrice = ref(690);
const displayedBirthdayPrice = ref(390);

let weddingPriceInterval = null;
watch(weddingPrice, (newPrice) => {
  if (weddingPriceInterval) clearInterval(weddingPriceInterval);
  const step = newPrice > displayedWeddingPrice.value ? 5 : -5;
  weddingPriceInterval = setInterval(() => {
    if (displayedWeddingPrice.value === newPrice) {
      clearInterval(weddingPriceInterval);
    } else {
      displayedWeddingPrice.value += step;
    }
  }, 12);
});

let birthdayPriceInterval = null;
watch(birthdayPrice, (newPrice) => {
  if (birthdayPriceInterval) clearInterval(birthdayPriceInterval);
  const step = newPrice > displayedBirthdayPrice.value ? 5 : -5;
  birthdayPriceInterval = setInterval(() => {
    if (displayedBirthdayPrice.value === newPrice) {
      clearInterval(birthdayPriceInterval);
    } else {
      displayedBirthdayPrice.value += step;
    }
  }, 12);
});

// Toast State
const toastOpen = ref(false);
const toastEmoji = ref('💍');
const toastTitle = ref('');
const toastDesc = ref('');
const toastIsWedding = ref(true);
let toastTimeout = null;

function showToast(emoji, title, desc, isWedding) {
  toastEmoji.value = emoji;
  toastTitle.value = title;
  toastDesc.value = desc;
  toastIsWedding.value = isWedding;
  toastOpen.value = true;
  
  if (toastTimeout) clearTimeout(toastTimeout);
  toastTimeout = setTimeout(() => {
    toastOpen.value = false;
  }, 4000);
}

// Particle system state
let weddingParticles = [];
let birthdayParticles = [];
let animationFrameWedding = null;
let animationFrameBirthday = null;
let intervalRice = null;

const colors = [
  'rgba(236, 72, 153, ',  // Pink
  'rgba(139, 92, 246, ',  // Purple
  'rgba(59, 130, 246, ',  // Blue
  'rgba(245, 158, 11, '   // Orange
];

// Classes
class RiceGrain {
  constructor(canvasWidth, canvasHeight, forceSide = null, isBurst = false) {
    this.canvasWidth = canvasWidth;
    this.canvasHeight = canvasHeight;
    this.isBurst = isBurst;
    
    this.side = forceSide || (Math.random() < 0.5 ? 'left' : 'right');
    this.y = canvasHeight * 0.40 + (Math.random() * 40 - 20);

    if (this.side === 'left') {
      this.x = Math.random() * 15 - 10;
      const angle = -Math.PI / 4.5 + (Math.random() * 0.25 - 0.12);
      const speed = isBurst ? (Math.random() * 10 + 9) : (Math.random() * 6.5 + 5.5);
      this.vx = Math.cos(angle) * speed;
      this.vy = Math.sin(angle) * speed;
    } else {
      this.x = canvasWidth + Math.random() * 15 - 5;
      const angle = -3.2 * Math.PI / 4 + (Math.random() * 0.25 - 0.12);
      const speed = isBurst ? (Math.random() * 10 + 9) : (Math.random() * 6.5 + 5.5);
      this.vx = Math.cos(angle) * speed;
      this.vy = Math.sin(angle) * speed;
    }

    this.width = Math.random() * 1.3 + 1.2;
    this.length = Math.random() * 3.5 + 4.5;
    this.rotation = Math.random() * Math.PI * 2;
    this.rotationSpeed = (Math.random() * 0.16 - 0.08);
    this.alpha = 1;
    this.decay = isBurst ? (Math.random() * 0.005 + 0.0025) : 0;
    this.color = `rgba(${245 + Math.random() * 10}, ${242 + Math.random() * 13}, ${230 + Math.random() * 15}, `;
  }

  update() {
    this.x += this.vx;
    this.y += this.vy;
    this.vy += 0.26; 
    this.rotation += this.rotationSpeed;

    if (this.decay > 0) {
      this.alpha -= this.decay;
    }
  }

  draw(ctx) {
    ctx.save();
    ctx.translate(this.x, this.y);
    ctx.rotate(this.rotation);
    ctx.beginPath();
    ctx.ellipse(0, 0, this.width, this.length / 2, 0, 0, Math.PI * 2);
    ctx.fillStyle = this.color + this.alpha + ')';
    ctx.shadowColor = '#ffffff';
    ctx.shadowBlur = 2.5;
    ctx.fill();
    ctx.restore();
  }
}

class Balloon {
  constructor(x, y, isBurst = false) {
    this.x = x;
    this.y = y;
    this.r = Math.random() * 8 + 10;
    this.color = colors[Math.floor(Math.random() * colors.length)];
    this.alpha = 1;
    
    if (isBurst) {
      this.vx = (Math.random() - 0.5) * 4;
      this.vy = -(Math.random() * 4 + 2);
    } else {
      this.vx = (Math.random() - 0.5) * 0.8;
      this.vy = -(Math.random() * 0.8 + 0.6);
    }
    
    this.wobbleSpeed = Math.random() * 0.03 + 0.01;
    this.wobbleValue = Math.random() * Math.PI;
    this.decay = isBurst ? 0.008 : 0;
  }

  update() {
    this.y += this.vy;
    this.wobbleValue += this.wobbleSpeed;
    this.x += this.vx + Math.sin(this.wobbleValue) * 0.12;
    if (this.decay > 0) this.alpha -= this.decay;
  }

  draw(ctx) {
    ctx.save();
    ctx.translate(this.x, this.y);
    ctx.globalAlpha = this.alpha;

    ctx.beginPath();
    ctx.moveTo(0, this.r * 1.2);
    ctx.bezierCurveTo(1.5, this.r * 1.5, -1.5, this.r * 1.7, 0, this.r * 2);
    ctx.strokeStyle = 'rgba(255, 255, 255, 0.15)';
    ctx.lineWidth = 0.6;
    ctx.stroke();

    ctx.beginPath();
    ctx.ellipse(0, 0, this.r * 0.85, this.r * 1.1, 0, 0, Math.PI * 2);
    ctx.fillStyle = this.color + '0.65)';
    ctx.fill();

    ctx.beginPath();
    ctx.ellipse(-this.r * 0.3, -this.r * 0.4, this.r * 0.15, this.r * 0.25, Math.PI / 4, 0, Math.PI * 2);
    ctx.fillStyle = 'rgba(255, 255, 255, 0.35)';
    ctx.fill();

    ctx.restore();
  }
}

class SoapBubble {
  constructor(x, y, isBurst = false) {
    this.x = x;
    this.y = y;
    this.r = Math.random() * 5 + 3;
    this.alpha = 1;
    
    if (isBurst) {
      this.vx = (Math.random() - 0.5) * 6;
      this.vy = -(Math.random() * 5 + 1.5);
    } else {
      this.vx = (Math.random() - 0.5) * 1;
      this.vy = -(Math.random() * 1 + 0.5);
    }
    
    this.wobbleValue = Math.random() * Math.PI;
    this.wobbleSpeed = Math.random() * 0.04 + 0.01;
    this.decay = isBurst ? 0.01 : 0;
  }

  update() {
    this.y += this.vy;
    this.wobbleValue += this.wobbleSpeed;
    this.x += this.vx + Math.sin(this.wobbleValue) * 0.2;
    if (this.decay > 0) this.alpha -= this.decay;
  }

  draw(ctx) {
    ctx.save();
    ctx.translate(this.x, this.y);
    ctx.globalAlpha = this.alpha;
    ctx.beginPath();
    ctx.arc(0, 0, this.r, 0, Math.PI * 2);
    
    let gradient = ctx.createRadialGradient(-this.r * 0.3, -this.r * 0.3, 1, 0, 0, this.r);
    gradient.addColorStop(0, 'rgba(255, 255, 255, 0.4)');
    gradient.addColorStop(0.6, 'rgba(236, 72, 153, 0.1)');
    gradient.addColorStop(0.8, 'rgba(59, 130, 246, 0.1)');
    gradient.addColorStop(1, 'rgba(255, 255, 255, 0.2)');
    
    ctx.fillStyle = gradient;
    ctx.strokeStyle = 'rgba(255, 255, 255, 0.3)';
    ctx.lineWidth = 0.5;
    ctx.fill();
    ctx.stroke();
    ctx.restore();
  }
}

function launchRicePoignee(side, count = 25, isBurst = false) {
  if (!weddingCanvas.value) return;
  const w = weddingCanvas.value.width;
  const h = weddingCanvas.value.height;
  for (let i = 0; i < count; i++) {
    setTimeout(() => {
      weddingParticles.push(new RiceGrain(w, h, side, isBurst));
    }, i * 10);
  }
}

function startRiceInterval() {
  if (intervalRice) clearInterval(intervalRice);
  intervalRice = setInterval(() => {
    launchRicePoignee('left', 18, false);
    setTimeout(() => {
      launchRicePoignee('right', 18, false);
    }, 300);
  }, 2000);
}

function animateWedding() {
  if (!weddingCanvas.value) return;
  const canvas = weddingCanvas.value;
  const ctx = canvas.getContext('2d');
  if (!ctx) return;
  
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  for (let i = weddingParticles.length - 1; i >= 0; i--) {
    const p = weddingParticles[i];
    p.update();
    p.draw(ctx);

    if (p.y > canvas.height + 20 || p.x < -30 || p.x > canvas.width + 30 || p.alpha <= 0) {
      weddingParticles.splice(i, 1);
    }
  }
  animationFrameWedding = requestAnimationFrame(animateWedding);
}

function animateBirthday() {
  if (!birthdayCanvas.value) return;
  const canvas = birthdayCanvas.value;
  const ctx = canvas.getContext('2d');
  if (!ctx) return;
  
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  if (birthdayParticles.length < 30 && Math.random() < 0.1) {
    if (Math.random() < 0.35) {
      birthdayParticles.push(new Balloon(Math.random() * canvas.width, canvas.height + 20, false));
    } else {
      birthdayParticles.push(new SoapBubble(Math.random() * canvas.width, canvas.height + 10, false));
    }
  }

  for (let i = birthdayParticles.length - 1; i >= 0; i--) {
    const p = birthdayParticles[i];
    p.update();
    p.draw(ctx);

    if (p.y < -30 || p.x < -30 || p.x > canvas.width + 30 || p.alpha <= 0) {
      birthdayParticles.splice(i, 1);
    }
  }
  animationFrameBirthday = requestAnimationFrame(animateBirthday);
}

// Option Wedding
function toggleWeddingOption(opt, event) {
  weddingOptions.value[opt] = !weddingOptions.value[opt];
  
  if (weddingOptions.value[opt]) {
    if (weddingCard.value && weddingCanvas.value) {
      const rect = weddingCard.value.getBoundingClientRect();
      const clickX = event.clientX - rect.left;
      const side = clickX < (weddingCanvas.value.width / 2) ? 'left' : 'right';
      launchRicePoignee(side, 15, true);
    }
  }
}

// Option Birthday
function toggleBirthdayOption(opt, event) {
  birthdayOptions.value[opt] = !birthdayOptions.value[opt];
  
  if (birthdayOptions.value[opt]) {
    if (birthdayCard.value && birthdayCanvas.value) {
      const rect = birthdayCard.value.getBoundingClientRect();
      const clickX = event.clientX - rect.left;
      const clickY = event.clientY - rect.top;
      for (let i = 0; i < 10; i++) {
        if (Math.random() < 0.5) {
          birthdayParticles.push(new Balloon(clickX, clickY, true));
        } else {
          birthdayParticles.push(new SoapBubble(clickX, clickY, true));
        }
      }
    }
  }
}

const weddingBtnText = ref('Réserver');
const birthdayBtnText = ref('Réserver');

function triggerWeddingPurchase(event) {
  if (weddingBtnText.value !== 'Réserver') return;

  // Vague 1 : Simultanée Gauche + Droite
  launchRicePoignee('left', 35, true);
  launchRicePoignee('right', 35, true);
  
  // Vague 2 : Gauche
  setTimeout(() => {
      launchRicePoignee('left', 25, true);
  }, 250);
  
  // Vague 3 : Droite
  setTimeout(() => {
      launchRicePoignee('right', 25, true);
  }, 500);

  // Vague 4 : Gauche
  setTimeout(() => {
      launchRicePoignee('left', 30, true);
  }, 750);

  // Vague 5 : Droite
  setTimeout(() => {
      launchRicePoignee('right', 30, true);
  }, 1000);

  weddingBtnText.value = "Traitement...";
  setTimeout(() => {
      weddingBtnText.value = "Réserver";
      showToast("💍", "Félicitations !", "Votre pack mariage est réservé. Vive les mariés !", true);
  }, 1200);

  let finalTitle = 'Pack "Fiançailles & Union"';
  const opts = [];
  if (weddingOptions.value.lights) opts.push('Lumières');
  if (weddingOptions.value.smoke) opts.push('Fumée');
  if (opts.length > 0) {
    finalTitle += ` + Option ${opts.join(' & ')}`;
  }

  emit('selectPack', { 
    type: 'mariage', 
    price: weddingPrice.value, 
    title: finalTitle 
  });
}

function triggerBirthdayPurchase(event) {
  if (birthdayBtnText.value !== 'Réserver') return;

  if (birthdayCanvas.value) {
    for (let i = 0; i < 25; i++) {
        birthdayParticles.push(new Balloon(Math.random() * birthdayCanvas.value.width, birthdayCanvas.value.height + 15, true));
        birthdayParticles.push(new SoapBubble(Math.random() * birthdayCanvas.value.width, birthdayCanvas.value.height + 10, true));
    }
  }

  birthdayBtnText.value = "Traitement...";
  setTimeout(() => {
      birthdayBtnText.value = "Réserver";
      showToast("🎂", "Joyeux Anniversaire !", "Votre pack VIP est réservé. Préparez la fête !", false);
  }, 1000);

  let finalTitle = 'Pack "Anniversaire VIP"';
  const opts = [];
  if (birthdayOptions.value.confetti) opts.push('Confettis');
  if (birthdayOptions.value.bubbles) opts.push('Mach. Bulles');
  if (opts.length > 0) {
    finalTitle += ` + Option ${opts.join(' & ')}`;
  }

  emit('selectPack', { 
    type: 'anniversaire', 
    price: birthdayPrice.value, 
    title: finalTitle 
  });
}

function resize() {
  if (weddingCanvas.value && weddingCard.value) {
    weddingCanvas.value.width = weddingCard.value.clientWidth;
    weddingCanvas.value.height = weddingCard.value.clientHeight;
  }
  if (birthdayCanvas.value && birthdayCard.value) {
    birthdayCanvas.value.width = birthdayCard.value.clientWidth;
    birthdayCanvas.value.height = birthdayCard.value.clientHeight;
  }
}

watch(activeTab, async (newTab) => {
  if (newTab === 'packs') {
    await nextTick();
    resize();
    if (!animationFrameWedding) animateWedding();
    if (!animationFrameBirthday) animateBirthday();
    startRiceInterval();
  } else {
    if (animationFrameWedding) {
      cancelAnimationFrame(animationFrameWedding);
      animationFrameWedding = null;
    }
    if (animationFrameBirthday) {
      cancelAnimationFrame(animationFrameBirthday);
      animationFrameBirthday = null;
    }
    if (intervalRice) {
      clearInterval(intervalRice);
      intervalRice = null;
    }
  }
});

onMounted(async () => {
  window.addEventListener('resize', resize);
  await nextTick();
  resize();
  
  if (activeTab.value === 'packs') {
    animateWedding();
    animateBirthday();
    startRiceInterval();
  }
});

onUnmounted(() => {
  window.removeEventListener('resize', resize);
  if (animationFrameWedding) cancelAnimationFrame(animationFrameWedding);
  if (animationFrameBirthday) cancelAnimationFrame(animationFrameBirthday);
  if (intervalRice) clearInterval(intervalRice);
  if (weddingPriceInterval) clearInterval(weddingPriceInterval);
  if (birthdayPriceInterval) clearInterval(birthdayPriceInterval);
});

function addItem(name, price) {
  emit('addItem', { name, price });
}
</script>
