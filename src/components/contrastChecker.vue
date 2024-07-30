<template>
  <div class="w-full flex flex-wrap lg:flex-nowrap items-center p-3">
    <div class="flex flex-col w-full lg:w-1/2 items-center justify-center p-6">
      <div class="mb-4 w-full">
        <label for="bg" class="block text-lg font-medium text-gray-700 dark:text-gray-300">Background Color</label>
        <input v-model="bg" id="bg" type="text"
          class="mt-1 block w-full placeholder:text-gray-600 dark:placeholder:text-gray-400 p-2 bg-gray-200 dark:bg-slate-800 rounded-md shadow-sm focus:ring-[#005ff0] focus:border focus:border-[#005ff0]"
          placeholder="#FFFFFF" />
      </div>
      <div class="mb-4 w-full">
        <label for="fg" class="block text-lg font-medium text-gray-700 dark:text-gray-300">Text Color</label>
        <input v-model="fg" id="fg" type="text"
          class="mt-1 block w-full placeholder:text-gray-600 dark:placeholder:text-gray-400 p-2 bg-gray-200 dark:bg-slate-800 rounded-md shadow-sm focus:ring-blue-600 focus:border focus:border-blue-600"
          placeholder="#000000" />
        <p class="mt-3 text-lg text-center text-gray-700 dark:text-gray-300">
          Contrast Ratio: <span class="font-bold text-blue-600">{{ contrastRatio.toFixed(2) }}</span>
        </p>
        <div class="sh ps ts mt-2 bg-gray-200 dark:bg-slate-800 px-20 py-10 text-2xl font-bold text-center rounded-md">
          <p>This color is <span
              :class="[contrastRatio >= 4.5 ? 'text-green-600 dark:text-green-500' : 'text-red-600 dark:text-red-500']">{{
                contrastRatio >= 4.5 ? 'Accessible' : 'Not Accessible' }}</span> according to WCAG (Web Content
            Accessibility Guidelines)</p>
        </div>
      </div>
    </div>
    <div class="flex flex-col w-full lg:w-1/2 items-center justify-center p-6">
      <div class="sh border border-black cs p-6 rounded-2xl h-[22.5rem] w-full"
        :style="{ backgroundColor: bg, color: fg }">
        <h1 class="hs text-[2rem] font-bold mb-4">Famous Quote</h1>
        <p class="ts text-[1.368rem]">“Good code is its own best documentation. As you’re about to add a comment, ask
          yourself, ‘How can I improve the code so that this comment isn’t needed?" <b>- Steve McConnell</b></p>
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

<style scoped>
@media (360px <=width <=640px) {
  .ts {
    /* text small */
    @apply text-base;
  }

  .hs {
    /* heading small */
    @apply text-lg;
  }

  .ps {
    /* padding small */
    @apply px-8 py-5;
  }

  .cs {
    /* container small */
    @apply h-auto;
  }
}

.sh {
  @apply shadow-sm shadow-black dark:shadow-white dark:border-none;
}
</style>