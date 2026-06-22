<template>
  <!-- Teleport the fixed elements to body so they are not constrained by any overflow hidden -->
  <Teleport to="body">
    <Transition name="chat-window">
      <div v-show="isOpen" class="fixed inset-0 sm:inset-auto sm:right-10 sm:bottom-[100px] w-full sm:w-[380px] h-[100dvh] sm:h-[550px] max-w-none sm:max-w-[calc(100vw-3rem)] max-h-none sm:max-h-[calc(100vh-8rem)] z-[120] rounded-none sm:rounded-2xl border border-gray-800/80 chat-window-bg overflow-hidden flex flex-col shadow-2xl origin-bottom-right">
        <!-- Header -->
        <div class="bg-dark-950/90 border-b border-gray-800/80 px-4 py-3 flex items-center justify-between">
          <div class="flex items-center space-x-2">
             <span class="w-2.5 h-2.5 rounded-full bg-neon-pink/70"></span>
             <span class="w-2.5 h-2.5 rounded-full bg-neon-yellow/70"></span>
             <span class="w-2.5 h-2.5 rounded-full bg-neon-emerald/70"></span>
             <span class="ml-3 text-[11px] font-bold text-gray-400 flex items-center gap-1.5 uppercase tracking-wider">
               <i class="fa-solid fa-message text-[10px] text-brand-400"></i> Assistant LMS
             </span>
          </div>
          <!-- Close button -->
          <button @click="isOpen = false" class="w-7 h-7 flex items-center justify-center rounded-full bg-white/5 hover:bg-white/10 text-gray-400 hover:text-white transition-colors cursor-pointer">
            <i class="fa-solid fa-xmark text-sm"></i>
          </button>
        </div>
        <ChatWidget 
          @switch-tab="closeChatAndScrollToForm" 
          @prefill-form="handlePrefillEvent" 
          @talking-status="handleTalkingStatus"
          class="flex-1 rounded-none border-none" 
        />
      </div>
    </Transition>

    <button 
      @click="isOpen = !isOpen"
      class="fixed z-[110] flex items-center justify-center transition-all duration-[700ms] chat-btn-anim cursor-pointer group shadow-[0_0_15px_rgba(139,92,246,0.25)] isolate floating-chat-btn"
      :class="[
        'bg-gradient-to-tr from-brand-600 to-neon-pink hover:from-brand-500 hover:to-neon-pink/95',
        !isOpen && showIntroBubble ? 'animate-strong-float' : (!isOpen ? 'animate-soft-float' : '')
      ]"
      :title="isOpen ? 'Fermer le chat' : 'Ouvrir le chat'"
    >
      <div class="absolute inset-0 bg-white/10 opacity-0 group-hover:opacity-100 transition-opacity duration-300 rounded-[inherit]"></div>

      <div class="relative z-10 flex flex-col items-center justify-center transition-all duration-300 h-full w-full pb-[14px]"
           :style="{ mixBlendMode: 'destination-out' }">
        <i class="fa-solid fa-robot text-2xl text-black"></i>
        
        <!-- The Mouth -->
        <div class="bg-black transition-all -mt-[5px]"
             :class="isTalking ? 'animate-mouth-talk' : 'w-[10px] h-[2.5px] rounded-full duration-300'">
        </div>
      </div>
    </button>

    <!-- Intro Bubble (placed outside button to avoid clip-path masking) -->
    <Transition name="fade-slide">
      <div 
        v-if="showIntroBubble && !isOpen" 
        @click.stop="isOpen = true; showIntroBubble = false"
        class="fixed z-[105] mr-4 w-56 sm:w-64 bg-dark-900 border border-brand-500/30 rounded-2xl p-3.5 shadow-xl shadow-brand-500/5 cursor-pointer hover:border-brand-500/60 transition-colors pointer-events-auto intro-bubble-fixed"
      >
        <div class="absolute right-[-6px] top-1/2 -translate-y-1/2 w-3 h-3 bg-dark-900 border-t border-r border-brand-500/30 rotate-45"></div>
        <p class="text-xs sm:text-sm text-gray-200 leading-relaxed relative z-10 text-left">
          <span class="text-neon-cyan font-bold mb-1 block flex items-center gap-1.5"><i class="fa-solid fa-robot mr-0.5"></i>Assistant LMS</span>
          {{ introPhrase }}
        </p>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup>
import { ref, watch, onMounted, onBeforeUnmount, nextTick } from 'vue';
import ChatWidget from './ChatWidget.vue';
import suggestionsConfig from '../data/suggestions.json';

const props = defineProps({
  isScrolled: Boolean
});

const isOpen = ref(false);
const showIntroBubble = ref(false);
const hasShownIntro = ref(false);
const introPhrase = suggestionsConfig.welcomeMessage;
let introTimeout = null;

const isTalking = ref(false);

const handleTalkingStatus = (status) => {
  isTalking.value = status.bot || status.user;
};

onMounted(() => {
  if (!hasShownIntro.value) {
    setTimeout(() => {
      if (!isOpen.value) {
        showIntroBubble.value = true;
        hasShownIntro.value = true;
        
        introTimeout = setTimeout(() => {
          showIntroBubble.value = false;
        }, 10000);
      }
    }, 2000);
  }
});

onBeforeUnmount(() => {
  if (introTimeout) clearTimeout(introTimeout);
});

watch(isOpen, (val) => {
  if (val) showIntroBubble.value = false;
});

const closeChatAndScrollToForm = () => {
  isOpen.value = false;
  document.getElementById('calculator')?.scrollIntoView({ behavior: 'smooth' });
};

const handlePrefillEvent = (data) => {
  isOpen.value = false;
  window.dispatchEvent(new CustomEvent('chat-prefill', { detail: data }));
  document.getElementById('calculator')?.scrollIntoView({ behavior: 'smooth' });
};
</script>

<style scoped>
.chat-window-bg {
  background: rgba(4, 6, 16, 0.95) !important;
}

@supports (backdrop-filter: blur(16px)) or (-webkit-backdrop-filter: blur(16px)) {
  .chat-window-bg {
    background: rgba(4, 6, 16, 0.85) !important;
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
  }
}

.chat-btn-anim {
  transition-timing-function: cubic-bezier(0.34, 1.56, 0.64, 1);
}

.floating-chat-btn {
  bottom: 24px;
  right: 24px;
  width: 56px;
  height: 70px; /* 56px body + 14px tail */
  clip-path: path('M 16 0 H 40 Q 56 0 56 16 V 48 Q 56 56 48 56 L 45 70 L 32 56 H 16 Q 0 56 0 40 V 16 Q 0 0 16 0 Z');
}

@media (min-width: 640px) {
  .floating-chat-btn {
    right: 40px;
  }
}

.chat-window-enter-active,
.chat-window-leave-active {
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}
.chat-window-enter-from,
.chat-window-leave-to {
  opacity: 0;
  transform: translateY(20px) scale(0.95);
  transform-origin: bottom right;
}

.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}
.fade-slide-enter-from,
.fade-slide-leave-to {
  opacity: 0;
  transform: translate(10px, 50%);
}

.intro-bubble-fixed {
  bottom: 66px; 
  right: 86px; 
  transform: translateY(50%);
}

@media (min-width: 640px) {
  .intro-bubble-fixed {
    right: 102px;
  }
}

@keyframes soft-float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-6px); }
}
.animate-soft-float {
  animation: soft-float 4s ease-in-out infinite;
}

@keyframes strong-float {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  25% { transform: translateY(-10px) rotate(-4deg); }
  50% { transform: translateY(0) rotate(0deg); }
  75% { transform: translateY(-10px) rotate(4deg); }
}
.animate-strong-float {
  animation: strong-float 1.5s ease-in-out infinite;
}

@keyframes mouth-talk {
  0% { height: 2.5px; width: 15px; border-radius: 9999px; }
  100% { height: 8px; width: 10px; border-radius: 50%; }
}
.animate-mouth-talk {
  animation: mouth-talk 0.15s infinite alternate;
}
</style>
