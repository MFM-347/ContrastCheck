<template>
    <div class="bgc bg-gray-100 dark:bg-slate-900 text-gray-950 dark:text-gray-200 flex flex-col items-center">
        <h1 class="text-3xl font-bold my-4">Color Contrast Checker</h1>
        <checker />
        <RouterLink to="/" class="absolute bottom-16 text-gray-500 dark:text-gray-400 text-lg my-4">&lt;&hyphen; Back
        </RouterLink>
    </div>
</template>
<script setup>
import checker from '@/components/contrastChecker.vue';
</script>