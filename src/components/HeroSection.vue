<template>
  <section class="relative overflow-hidden pt-6 pb-14 lg:py-20">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
          <div class="grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
              
              <!-- Left Hero Text -->
              <div class="lg:col-span-7 space-y-6 text-center lg:text-left">
                  <div class="inline-flex items-center gap-1.5 bg-brand-500/10 border border-brand-500/30 text-brand-300 px-3 py-1 rounded-full text-xs font-bold uppercase tracking-wider">
                      🎧 Le Pro de l'ambiance en Loire-Atlantique & Ille-et-Vilaine
                  </div>
                  
                  <h1 class="text-3xl sm:text-5xl lg:text-6.5xl font-extrabold text-white leading-tight tracking-tight">
                      Ne risquez pas le son de votre <span class="text-transparent bg-clip-text bg-gradient-to-r from-neon-pink via-brand-400 to-neon-cyan">soirée événementielle.</span>
                  </h1>
                  
                  <p class="text-sm sm:text-base lg:text-lg text-gray-400 font-light max-w-xl mx-auto lg:mx-0 leading-relaxed">
                      Packs de sonorisation de grande puissance et éclairages de club pré-configurés pour vos événements. 
                      À emporter gratuitement ou livré et installé à <span class="text-brand-300 font-semibold">Redon, Rennes, Nantes et La Baule.</span>
                  </p>

                  <!-- Wave Visual -->
                  <div class="flex items-center justify-center lg:justify-start gap-1">
                      <span class="text-xs text-gray-500 font-bold uppercase tracking-wider mr-2">Ambiance LMS :</span>
                      <div class="flex items-end gap-1 h-5">
                          <span class="w-1 bg-neon-pink h-2 animate-bounce" style="animation-duration: 0.6s"></span>
                          <span class="w-1 bg-brand-500 h-4 animate-bounce" style="animation-duration: 0.9s"></span>
                          <span class="w-1 bg-neon-cyan h-3 animate-bounce" style="animation-duration: 0.7s"></span>
                          <span class="w-1 bg-brand-400 h-5 animate-bounce" style="animation-duration: 1.1s"></span>
                      </div>
                  </div>

                  <!-- CTAs -->
                  <div class="flex flex-col sm:flex-row items-center justify-center lg:justify-start gap-3 pt-2">
                      <button @click="$emit('trigger-lights', 'offres')" class="w-full sm:w-auto text-center bg-gradient-to-r from-brand-600 to-indigo-600 text-white font-black uppercase text-xs px-6 py-4 rounded-xl border-b-4 border-brand-700 active:border-b-0 transition-all tracking-wider flex items-center justify-center gap-2 shadow-lg hover:shadow-brand-500/20">
                          <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><circle cx="12" cy="12" r="10"></circle><path d="M12 8v8M8 12h8"></path></svg> Parcourir nos offres
                      </button>
                      <button @click="$emit('trigger-lights', 'calculator')" class="w-full sm:w-auto text-center border border-gray-800 text-gray-300 font-bold text-xs uppercase tracking-wider px-6 py-4 rounded-xl hover:text-white bg-dark-900/40">
                          Simuler un devis direct
                      </button>
                  </div>
              </div>

              <!-- Right Visual Showcase Column -->
              <div class="lg:col-span-5 relative mt-6 lg:mt-0">
                  <div class="relative mx-auto max-w-sm bg-dark-900/90 border border-gray-800 p-5 rounded-3xl shadow-2xl overflow-hidden group">
                      <div class="absolute inset-0 bg-gradient-to-tr from-brand-600/10 to-neon-pink/10 opacity-50 pointer-events-none"></div>
                      <div class="aspect-square w-full rounded-2xl overflow-hidden bg-dark-950 border border-gray-800/80 relative flex flex-col items-center justify-center p-8 space-y-8">
                          <div class="relative w-full h-full flex flex-col justify-between">
                              <!-- Top status badge -->
                              <div class="flex justify-between items-center w-full">
                                  <span class="text-[10px] font-bold text-neon-cyan tracking-widest uppercase bg-neon-cyan/10 px-2.5 py-1 rounded border border-neon-cyan/20">Système Premium</span>
                                  <span class="flex h-2 w-2 relative">
                                      <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75"></span>
                                      <span class="relative inline-flex rounded-full h-2 w-2 bg-emerald-500"></span>
                                  </span>
                              </div>
                              
                              <!-- Visual graphic of pro speaker gear -->
                              <div class="flex items-center justify-center py-4">
                                  <svg class="w-28 h-28 text-gray-400 drop-shadow-[0_0_15px_rgba(139,92,246,0.25)] animate-speaker-bounce" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round">
                                      <rect x="5" y="2" width="14" height="20" rx="2" stroke="currentColor" stroke-width="1.5"></rect>
                                      <circle cx="12" cy="7.5" r="1.5" fill="currentColor"></circle>
                                      <circle cx="12" cy="15" r="3.5" stroke="currentColor" stroke-width="1.5"></circle>
                                      <circle cx="12" cy="15" r="1.5" fill="currentColor"></circle>
                                  </svg>
                              </div>
                              
                              <!-- Gear subtitle -->
                              <div class="space-y-1 text-center">
                                  <h4 class="text-xs font-bold text-white uppercase tracking-wider">Sonorisation JBL & HK Audio</h4>
                                  <p class="text-[10px] text-gray-500 leading-relaxed">Pression acoustique optimale et clarté sonore garantie.</p>
                              </div>
                          </div>
                      </div>
                  </div>
              </div>

          </div>
      </div>
  </section>

  <!-- Zone d'Ancrage Local (SEO) -->
  <section class="bg-dark-900 border-y border-gray-800/80 py-4 text-center">
      <div class="max-w-7xl mx-auto px-4 text-xs font-semibold tracking-wider text-gray-500 uppercase flex flex-wrap justify-center gap-3">
          <span>📍 Redon (35)</span>
          <span>📍 Rennes / Ille-et-Vilaine</span>
          <span>📍 Nantes / Loire-Atlantique</span>
          <span>📍 La Baule / Presqu'île de Guérande</span>
      </div>
  </section>
</template>

<script setup>
</script>
