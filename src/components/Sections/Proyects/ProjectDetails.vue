<template>
    <div ref="detailPanel"
        class="fixed inset-0 z-[100] hidden bg-slate-900 flex-col items-center justify-center text-center p-10"
        style="clip-path: circle(0% at 50% 50%);">
        <button @click="closePanel"
            class="absolute top-10 right-10 text-white text-4xl hover:rotate-90 transition-transform">✕</button>

        <div v-if="project" class="max-w-3xl">
            <p class="detail-content text-emerald-400 font-mono mb-4">{{ project.category }}</p>
            <h2 class="detail-content text-white text-7xl font-black mb-8">{{ project.title }}</h2>
            <p class="detail-content text-slate-400 text-xl mb-10">{{ project.desc }}</p>

            <div v-if="project.icons && project.icons.length > 0"
                class="detail-content flex flex-wrap gap-4 justify-center mb-12">
                <div v-for="(icon, index) in project.icons" :key="index"
                    class="icon-wrapper w-14 h-14 bg-slate-800/80 border border-slate-700 rounded-2xl flex items-center justify-center p-3 hover:-translate-y-2 hover:bg-slate-700 hover:shadow-emerald-500/20 hover:shadow-lg hover:border-emerald-500/50 transition-all duration-300"
                    v-html="icon"></div>
            </div>

            <div class="detail-content flex gap-6 justify-center">
                <a :href="project.link" target="_blank"
                    class="bg-emerald-500 text-slate-950 px-10 py-4 rounded-full font-bold hover:bg-white transition-colors">
                    Visitar Web en Vivo
                </a>
                <button @click="closePanel"
                    class="border border-white/20 text-white px-10 py-4 rounded-full hover:bg-white/10">
                    Volver
                </button>
            </div>
        </div>
    </div>
</template>

<script>
import { gsap } from 'gsap';

export default {
    name: 'ProjectDetails',
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
