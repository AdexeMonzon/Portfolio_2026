

<template>
    <section ref="scrollWrapper" class="relative bg-slate-950 min-h-screen py-32 px-[5vw] md:px-[10vw]">

        <div class="mb-16 title-container">
            <p class="text-white text-6xl md:text-7xl font-black leading-none uppercase tracking-tighter">
                Mis <br> <span
                    class="text-transparent bg-clip-text bg-gradient-to-r from-emerald-400 to-cyan-500">Proyectos</span>
            </p>
        </div>

        <div class="grid grid-cols-1 xl:grid-cols-2 gap-12">
            <div v-for="project in projects" :key="project.id"
                class="project-card h-[65vh] bg-slate-900 rounded-3xl overflow-hidden relative group">
                <img :src="project.img"
                    class="w-full h-full object-cover opacity-40 group-hover:opacity-100 group-hover:scale-105 transition-all duration-700" />

                <div
                    class="absolute inset-0 p-8 md:p-12 flex flex-col justify-end bg-gradient-to-t from-black/90 via-transparent to-transparent">
                    <div class="translate-y-8 group-hover:translate-y-0 transition-transform duration-500">
                        <p class="text-emerald-400 font-mono text-sm mb-3">{{ project.category }}</p>
                        <h3 class="text-white text-4xl md:text-5xl font-bold mb-6">{{ project.title }}</h3>

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

        <ProjectDetails ref="detailsComponent" :project="selectedProject" @closed="selectedProject = null" />

        <div class="h-[70vh] w-full flex items-center justify-center border-t border-white/5 mt-32">
            <p class="text-white/20 font-mono text-sm"></p>
        </div>

    </section>
</template>

<script>
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import ProjectDetails from './ProjectDetails.vue';
import { projectsData } from '../../../data/projects.js';

gsap.registerPlugin(ScrollTrigger);

export default {
    name: 'ProjectsView',
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
        this.initScrollAnimations();
    },
    methods: {
        initScrollAnimations() {
            gsap.fromTo(".title-container", 
                { y: 150, opacity: 0 },
                {
                    y: 0,
                    opacity: 1,
                    ease: "none",
                    scrollTrigger: {
                        trigger: this.$refs.scrollWrapper,
                        start: "top 85%", 
                        end: "top 30%",
                        scrub: 1
                    }
                }
            );

            const cards = gsap.utils.toArray(".project-card");
            
            cards.forEach((card) => {
                gsap.fromTo(card, 
                    { 
                        y: 50,
                        opacity: 0,
                        scale: 0.95
                    }, 
                    {
                        y: -50,
                        opacity: 1,
                        scale: 1,
                        ease: "none",
                        scrollTrigger: {
                            trigger: card,
                            start: "top 95%",
                            end: "top 40%",
                            scrub: 1
                        }
                    }
                );
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