<template>
  <div ref="container" class="typewriter-content" v-html="displayedText"></div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue';

const props = defineProps({
  htmlContent: {
    type: String,
    required: true,
  },
  speed: {
    type: Number,
    default: 8, // Vitesse de frappe fluide en ms
  },
});

const emit = defineEmits(['finished']);
const displayedText = ref('');
const container = ref(null);

const runTypewriter = () => {
  const html = props.htmlContent;
  let i = 0;
  let isTag = false;
  let timeoutId = null;

  const draw = () => {
    if (i >= html.length) {
      emit('finished');
      return;
    }
    const char = html[i];
    if (char === '<') isTag = true;
    if (char === '>') {
      isTag = false;
      displayedText.value = html.substring(0, i + 1);
      i++;
      draw();
      return;
    }

    displayedText.value = html.substring(0, i + 1);
    i++;

    if (isTag) {
      draw(); // Affiche instantanément les balises HTML sans délai
    } else {
      timeoutId = setTimeout(draw, props.speed);
    }
  };

  draw();

  return () => {
    if (timeoutId) clearTimeout(timeoutId);
  };
};

let cleanup = null;
onMounted(() => {
  cleanup = runTypewriter();
});

// Nettoyage en cas de démontage du composant
watch(() => props.htmlContent, () => {
  if (cleanup) cleanup();
  cleanup = runTypewriter();
});
</script>

<style scoped>
.typewriter-content {
  display: inline-block;
  width: 100%;
}
</style>
