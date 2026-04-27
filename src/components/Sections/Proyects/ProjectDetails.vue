<template>
    <div ref="detailPanel"
        class="fixed inset-0 z-[100] hidden bg-slate-950/95 backdrop-blur-xl flex-col items-center justify-center p-6 md:p-12 overflow-y-auto"
        style="clip-path: circle(0% at 50% 50%);">

        <button @click="closePanel"
            class="absolute top-9 right-8 text-slate-400 hover:text-white text-4xl hover:rotate-90 transition-all duration-300 z-50">✕</button>

        <div v-if="project"
            class="max-w-7xl w-full flex flex-col lg:flex-row gap-12 lg:gap-20 items-center mt-20 lg:mt-0">

            <!-- Izquierda: Información -->
            <div class="flex-1 text-left">
                <p class="detail-content text-emerald-400 font-mono mb-4 text-sm md:text-lg tracking-widest uppercase">
                    {{ project.category }}</p>
                <h2 class="detail-content text-white text-5xl md:text-7xl font-black mb-8 leading-tight">{{
                    project.title }}</h2>
                <p class="detail-content text-slate-300 text-lg md:text-xl mb-12 leading-relaxed font-light">{{
                    project.desc }}</p>

                <!-- Tecnologías -->
                <div v-if="project.icons && project.icons.length > 0" class="detail-content mb-14">
                    <h3 class="text-xs text-slate-500 uppercase tracking-widest font-mono mb-6">Tecnologías Utilizadas
                    </h3>
                    <div class="flex flex-wrap gap-4">
                        <div v-for="(icon, index) in project.icons" :key="index"
                            class="icon-wrapper w-14 h-14 bg-slate-800/80 border border-slate-700 rounded-xl flex items-center justify-center p-3 hover:-translate-y-2 hover:bg-slate-700 hover:shadow-emerald-500/20 hover:shadow-lg hover:border-emerald-500/50 transition-all duration-300"
                            v-html="icon"></div>
                    </div>
                </div>

                <!-- Enlaces -->
                <div class="detail-content flex flex-wrap gap-4">
                    <a v-if="project.website" :href="project.website" target="_blank"
                        class="bg-emerald-500 text-slate-950 px-8 py-4 rounded-full font-bold hover:bg-emerald-400 transition-colors flex items-center gap-2 shadow-lg shadow-emerald-500/20">
                        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path>
                        </svg>
                        Visitar Web
                    </a>

                    <a v-if="project.githubFrontend" :href="project.githubFrontend" target="_blank"
                        class="border border-slate-600 text-white px-8 py-4 rounded-full hover:bg-slate-800 hover:border-slate-400 transition-all flex items-center gap-2">
                        <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                            <path fill-rule="evenodd"
                                d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"
                                clip-rule="evenodd"></path>
                        </svg>
                        Frontend
                    </a>

                    <a v-if="project.githubBackend" :href="project.githubBackend" target="_blank"
                        class="border border-slate-600 text-white px-8 py-4 rounded-full hover:bg-slate-800 hover:border-slate-400 transition-all flex items-center gap-2">
                        <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                            <path fill-rule="evenodd"
                                d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"
                                clip-rule="evenodd"></path>
                        </svg>
                        Backend
                    </a>
                </div>
            </div>

            <!-- Derecha: Imagen del Proyecto -->
            <div class="flex-1 w-full detail-content flex justify-center lg:justify-end">
                <div
                    class="relative w-full max-w-md lg:max-w-lg rounded-[2rem] overflow-hidden border border-slate-800/50 shadow-2xl shadow-emerald-500/10 group">
                    <div
                        class="absolute inset-0 bg-gradient-to-tr from-emerald-500/10 to-transparent mix-blend-overlay group-hover:opacity-0 transition-opacity duration-700 z-10 pointer-events-none">
                    </div>
                    <Swiper :images="project.images" class="w-full h-auto object-cover" />
                </div>
            </div>



        </div>
    </div>
</template>

<script>
import { gsap } from 'gsap';
import Swiper from '../../share/swiper-slider.vue';

export default {
    name: 'ProjectDetails',
    components: {
        Swiper
    },
    props: {
        project: {
            type: Object,
            default: null
        }
    },
    methods: {
        open() {
            document.body.style.overflow = 'hidden';
            const tl = gsap.timeline();
            tl.to(this.$refs.detailPanel, {
                display: 'flex',
                duration: 0
            })
                .fromTo(this.$refs.detailPanel,
                    { clipPath: 'circle(0% at 50% 50%)' },
                    { clipPath: 'circle(150% at 50% 50%)', duration: 1, ease: 'expo.inOut' }
                )
                .fromTo(this.$el.querySelectorAll('.detail-content'), {
                    y: 50,
                    opacity: 0
                }, {
                    y: 0,
                    opacity: 1,
                    stagger: 0.1,
                    duration: 0.5
                });
        },
        closePanel() {
            const tl = gsap.timeline({
                onComplete: () => {
                    document.body.style.overflow = 'auto';
                    gsap.set(this.$refs.detailPanel, { display: 'none' });
                    this.$emit('closed');
                }
            });

            tl.to(this.$refs.detailPanel, {
                clipPath: 'circle(0% at 50% 50%)',
                duration: 0.8,
                ease: 'expo.inOut'
            });
        }
    }
}
</script>

<style lang="scss">
.icon-wrapper {

    img,
    svg {
        width: 100%;
        height: 100%;
        object-fit: contain;
    }
}
</style>
