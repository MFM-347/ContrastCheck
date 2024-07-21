<template>
  <div class="w-full flex flex-wrap lg:flex-nowrap items-center p-3">
    <div class="flex flex-col w-full lg:w-1/2 items-center justify-center p-6">
      <div class="mb-4 w-full">
        <label for="bg" class="block text-lg font-medium text-gray-700 dark:text-gray-300">Background Color</label>
        <input v-model="bg" id="bg" type="text" class="mt-1 block w-full placeholder:text-gray-600 dark:placeholder:text-gray-400 p-2 bg-gray-200 dark:bg-slate-800 rounded-md shadow-sm focus:ring-[#005ff0] focus:border focus:border-[#005ff0]" placeholder="#FFFFFF" />
      </div>
      <div class="mb-4 w-full">
        <label for="fg" class="block text-lg font-medium text-gray-700 dark:text-gray-300">Text Color</label>
        <input v-model="fg" id="fg" type="text" class="mt-1 block w-full placeholder:text-gray-600 dark:placeholder:text-gray-400 p-2 bg-gray-200 dark:bg-slate-800 rounded-md shadow-sm focus:ring-[#005ff0] focus:border focus:border-[#005ff0]" placeholder="#000000" />
        <p class="mt-4 text-lg text-center text-gray-700 dark:text-gray-300">
          Contrast Ratio: <span class="font-bold dark:text-[#83d5ff] text-[#005ff0]">{{ contrastRatio.toFixed(2) }}</span>
        </p>
        <div class="mt-2 bg-gray-200 dark:bg-slate-800 px-24 py-12 text-2xl font-bold text-center rounded-md shadow-md">
          <p>This color is <span :class="[contrastRatio >= 4.5 ? 'text-green-600 dark:text-green-500' : 'text-red-600 dark:text-red-500']">{{ contrastRatio >= 4.5 ? 'Accessible' : 'Not Accessible' }}</span> according to WCAG (Web Content Accessibility Guidelines)</p>
        </div>
      </div>
    </div>
    <div class="flex flex-col w-full lg:w-1/2 items-center justify-center p-6">
      <div class="p-6 rounded-2xl h-[22.5rem] w-[36rem]" :style="{ backgroundColor: bg, color: fg }">
        <h1 class="text-[2rem] font-bold mb-4">Famous Quote</h1>
        <p class="text-[1.368rem]">“Good code is its own best documentation. As you’re about to add a comment, ask yourself, ‘How can I improve the code so that this comment isn’t needed?" <b>- Steve McConnell</b></p>
      </div>
    </div>
  </div>
</template>

<script>
import tinycolor from 'tinycolor2';

export default {
  data() {
    return {
      bg: '#f0f0f6',
      fg: '#17171f',
    };
  },
  computed: {
    contrastRatio() {
      return tinycolor.readability(this.bg, this.fg);
    },
  },
};
</script>