<template>
    <section id="home" class="h-screen">
        <div>
            <Navbar />
        </div>
        <div>
            <header class="relative pt-16">
                <div class="container mx-auto">
                    <h1 class="text-6xl sm:text-7xl md:text-8xl font-extrabold tracking-tighter leading-none">
                        <span class="block text-white">Hello, I'm</span>
                        <span class="block text-emerald-400">Adexe Monzón Santana</span>
                    </h1>
                </div>
            </header>
        </div>
        <div class="h-[70vh] w-full flex items-center justify-center border-t border-white/5 mt-32">
            <p class="text-white/20 font-mono text-sm"></p>
        </div>
        <div>
            <Proyects />
        </div>

    </section>
</template>

<script>
import Navbar from '../../share/nav-component.vue';
import Proyects from '../Proyects/index.vue';
import Swiper from '../../share/swiper-slider.vue';

    export default {
        name: 'Home',
        components: {
            Navbar,
            Proyects,
            Swiper
        }
    }
</script>

<style lang="scss" scoped>

</style>