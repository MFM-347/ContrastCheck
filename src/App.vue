<template>
  <div class="bgc bg-gray-100 dark:bg-slate-900 text-gray-950 dark:text-gray-200 flex flex-col items-center">
    <h1 class="text-3xl font-bold my-4">Color Contrast Checker</h1>
    <button v-if="isInstallable" @click="installPWA" class="px-7 py-1 font-bold bg-blue-600 text-gray-200 hover:bg-blue-500 dark:bg-blue-400 dark:text-gray-900 rounded absolute top-4 right-[22.5rem]" id="install-pwa-btn" aria-label="Install PWA"><img src="/PWA.svg" class="h-8"></button>
    <checker />
  </div>
</template>
<script setup>
import { ref, onMounted } from 'vue';
import checker from '@/components/contrastChecker.vue';

const isInstallable = ref(false);
let deferredPrompt;

onMounted(() => {
  window.addEventListener('beforeinstallprompt', (e) => {
    e.preventDefault();
    deferredPrompt = e;
    isInstallable.value = true;
  });
});

function installPWA() {
  if (deferredPrompt) {
    deferredPrompt.prompt();
    deferredPrompt.userChoice.then((choiceResult) => {
      if (choiceResult.outcome === 'accepted') {
        isInstallable.value = false;
      }
      deferredPrompt = null;
    });
  }
}
</script>