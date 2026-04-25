

<template>
    <section ref="scrollWrapper" class="relative overflow-hidden bg-slate-950 min-h-screen">

        <div class="flex h-screen items-center px-[10vw]">
            <div class="flex-shrink-0 w-[40vw] pr-20">
                <h2 class="text-emerald-400 font-mono text-sm mb-4 tracking-widest uppercase">Proyectos</h2>
                <p class="text-white text-7xl font-black leading-none uppercase tracking-tighter">
                    Work <br> <span
                        class="text-transparent bg-clip-text bg-gradient-to-r from-emerald-400 to-cyan-500">Lab</span>
                </p>
            </div>

            <div class="flex gap-12">
                <div v-for="project in projects" :key="project.id"
                    class="project-card w-[50vw] h-[65vh] flex-shrink-0 bg-slate-900 rounded-3xl overflow-hidden relative group">
                    <img :src="project.img"
                        class="w-full h-full object-cover opacity-40 group-hover:opacity-100 group-hover:scale-105 transition-all duration-700" />

                    <div
                        class="absolute inset-0 p-12 flex flex-col justify-end bg-gradient-to-t from-black/90 via-transparent to-transparent">
                        <div class="translate-y-8 group-hover:translate-y-0 transition-transform duration-500">
                            <p class="text-emerald-400 font-mono text-sm mb-3">{{ project.category }}</p>
                            <h3 class="text-white text-5xl font-bold mb-6">{{ project.title }}</h3>

                            <button @click="openProject(project)" class="flex items-center gap-4 text-white group/btn">
                                <span
                                    class="w-12 h-12 rounded-full border border-white/20 flex items-center justify-center group-hover/btn:bg-white group-hover/btn:text-black transition-all">
                                    →
                                </span>
                                <span class="font-semibold tracking-wide uppercase text-xs">Ver Proyecto</span>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <ProjectDetails ref="detailsComponent" :project="selectedProject" @closed="selectedProject = null" />

    </section>
</template>

<script>
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { animate, inView, stagger } from 'motion';
import ProjectDetails from './ProjectDetails.vue';
import { projectsData } from '../../../data/projects.js';

gsap.registerPlugin(ScrollTrigger);

export default {
    name: 'HorizontalProjects',
    components: {
        ProjectDetails
    },
    data() {
        return {
            selectedProject: null,
            projects: projectsData
        };
    },
    mounted() {
        this.initHorizontalScroll();
        this.initMotionEntrance();
    },
    methods: {
        initHorizontalScroll() {
            const sections = gsap.utils.toArray(".project-card");
            gsap.to(sections, {
                xPercent: -100 * (sections.length - 1),
                ease: "none",
                scrollTrigger: {
                    trigger: this.$refs.scrollWrapper,
                    pin: true,
                    scrub: 1,
                    snap: 1 / (sections.length - 1),
                    end: () => "+=" + this.$refs.scrollWrapper.offsetWidth,
                }
            });
        },

        initMotionEntrance() {
            inView(this.$refs.scrollWrapper, () => {
                animate(".project-card", { opacity: [0, 1], y: [100, 0], scale: [0.8, 1] },
                    { delay: stagger(0.2), duration: 0.8, easing: [0.17, 0.55, 0.55, 1] });
            });
        },

        openProject(project) {
            this.selectedProject = project;

            /*  llamamos al método open del componente hijo de forma reactiva
            *   basicamente funciona de la siguiente manera: 
            *   ref es una referencia a un elemento del dom o a un componente
            *   nextTick es una función que permite ejecutar código después de que el dom haya sido actualizado
            *   asi que en resumen llamamos al metodo open del componente hijo de forma reactiva
            */
            this.$nextTick(() => {
                if (this.$refs.detailsComponent) {
                    this.$refs.detailsComponent.open();
                }
            });
        }
    }
};
</script>

<style scoped>
.project-card {
    will-change: transform, opacity;
}
</style>