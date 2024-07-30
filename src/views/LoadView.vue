<template>
    <div class="h-full grid place-items-center bg-blue-600">
        <div v-if="isVisible" class="rect">
            <div class="r r1"></div>
            <div class="r r2"></div>
        </div>
        <RouterLink v-else class="btn transition-colors duration-200 ease-in" to="/App">Start</RouterLink>
        <button v-if="isInstallable" @click="installPWA" class="btn transition-colors duration-200 ease-in"
            id="install-pwa-btn" aria-label="Install PWA">
            <img src="/PWA.svg" alt="Install PWA" class="h-8">
        </button>
    </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import anime from 'animejs/lib/anime.es.js';

export default {
    setup() {
        const isInstallable = ref(false);
        let deferredPrompt = null;

        onMounted(() => {
            window.addEventListener('beforeinstallprompt', (e) => {
                e.preventDefault();
                deferredPrompt = e;
                isInstallable.value = true;
            });
        });

        const installPWA = () => {
            if (deferredPrompt) {
                deferredPrompt.prompt();
                deferredPrompt.userChoice.then((choiceResult) => {
                    if (choiceResult.outcome === 'accepted') {
                        isInstallable.value = false;
                    }
                    deferredPrompt = null;
                });
            }
        };

        return { isInstallable, installPWA };
    },
    data() {
        return {
            isVisible: true,
        };
    },
    mounted() {
        this.animateLoader();
    },
    methods: {
        animateLoader() {
            anime({
                targets: document.querySelector('.rect'),
                rotate: '3turn',
                duration: 1000,
                loop: false,
                direction: 'alternate',
                complete: () => {
                    this.x1();
                    this.x2();
                }
            });
        },
        x1() {
            anime({
                targets: document.querySelector('.r1'),
                translateX: 59.25,
                duration: 1000,
                loop: false,
                complete: () => {
                    this.isVisible = false;
                }
            });
        },
        x2() {
            anime({
                targets: document.querySelector('.r2'),
                translateX: -59.25,
                duration: 1000,
                loop: false,
                complete: () => {
                    this.isVisible = false;
                }
            });
        }
    }
}
</script>

<style scoped>
.rect {
    @apply flex flex-row gap-x-2;
}

.r {
    @apply h-[3.25rem] border-4 border-gray-200;
}

.btn {
    @apply text-3xl py-2 px-4 border-x-8 border-gray-200 bg-blue-600 hover:bg-gray-200 hover:text-blue-600;
}
</style>