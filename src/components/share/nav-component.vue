<template>
    <nav ref="navContainer" :class="[
        'fixed top-0 left-0 w-full z-50 px-8 py-5 flex justify-between items-center transition-all duration-500',
        isScrolled ? 'backdrop-blur-xl bg-slate-950/80 py-3 border-b border-white/10' : 'bg-transparent'
    ]">
        <div class="group cursor-pointer">
            <h1 class="text-2xl font-black tracking-tighter text-white">
                ADEXE<span class="text-emerald-400 group-hover:animate-pulse">.</span>
            </h1>
        </div>

        <ul class="hidden md:flex items-center gap-10">
            <li v-for="item in menuItems" :key="item.name" class="nav-item">
                <a :href="item.href"
                    class="relative text-sm font-medium text-slate-300 hover:text-white transition-colors duration-300 group">
                    {{ item.name }}
                    <span
                        class="absolute -bottom-1 left-0 w-0 h-0.5 bg-emerald-400 transition-all duration-300 group-hover:w-full"></span>
                </a>
            </li>
        </ul>

        <div class="nav-item">
            <a href="#contact"
                class="bg-white text-slate-950 px-6 py-2.5 rounded-full font-bold text-sm hover:bg-emerald-400 hover:scale-105 transition-all duration-300 active:scale-95 inline-block">
                Empezar proyecto
            </a>
        </div>
    </nav>
</template>

<script>
import { gsap } from 'gsap';

export default {
    name: 'Navbar',

    data() {
        return {
            menuItems: [
                { name: 'Inicio', href: '#' },
                { name: 'Proyectos', href: '#projects' },
                { name: 'Sobre mí', href: '#about' },
                { name: 'Contacto', href: '#contact' },
            ],
            isScrolled: false
        };
    },

    mounted() {
        this.initAnimation();
        window.addEventListener('scroll', this.handleScroll);
    },

    unmounted() {
        window.removeEventListener('scroll', this.handleScroll);
    },

    methods: {
        initAnimation() {
            const tl = gsap.timeline();

            tl.from(this.$refs.navContainer, {
                y: -100,
                opacity: 0,
                duration: 1,
                ease: 'expo.out',
            })
                .from('.nav-item', {
                    y: -20,
                    opacity: 1,
                    duration: 0.6,
                    stagger: 0.1,
                    ease: 'back.out(1.7)',
                }, "-=0.7");
        },

        handleScroll() {
            this.isScrolled = window.scrollY > 50;
        }
    }
};
</script>

<style scoped></style>