<template>
    <section ref="scrollWrapper" class="proyects-section">

        <div class="proyects-title-container title-container">
            <p class="proyects-title">
                Mis <br> <ShinyText text="Proyectos" class="text-emerald" color="var(--accent)" shineColor="#B5FFE3" :speed="3" />
            </p>
        </div>

        <div class="proyects-grid">
            <div v-for="project in projects" :key="project.id" class="project-card group">
                <img :src="project.img" class="project-img" />

                <div class="project-overlay">
                    <div class="project-content">
                        <p class="project-category">{{ project.category }}</p>
                        <h3 class="project-title">{{ project.title }}</h3>

                        <button @click="openProject(project)" class="project-btn group-btn">
                            <span class="project-btn-icon">
                                →
                            </span>
                            <span class="project-btn-text">Ver Proyecto</span>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <ProjectDetails ref="detailsComponent" :project="selectedProject" @closed="selectedProject = null" />

        <div class="proyects-spacer"></div>

    </section>
</template>

<script>
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import ProjectDetails from './ProjectDetails.vue';
import { projectsData } from '../../../data/projects.js';
import ShinyText from '../../share/ShinyText.vue';

gsap.registerPlugin(ScrollTrigger);

export default {
    name: 'ProjectsView',
    components: {
        ProjectDetails,
        ShinyText
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
                    ease: "power3.out",
                    duration: 1,
                    scrollTrigger: {
                        trigger: this.$refs.scrollWrapper,
                        start: "top 80%",
                    }
                }
            );

            gsap.set(".project-card", { y: 100, opacity: 0, scale: 0.95 });

            ScrollTrigger.batch(".project-card", {
                start: "top 85%",
                onEnter: batch => gsap.to(batch, {
                    opacity: 1,
                    y: 0,
                    scale: 1,
                    duration: 1,
                    ease: "power3.out",
                    stagger: 0.2,
                    overwrite: true
                }),
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
.proyects-section {
    position: relative;
    background-color: transparent;
    color: var(--text-primary);
    font-family: sans-serif;
    min-height: 100vh;
    padding: 8rem 5vw;
}

@media (min-width: 768px) {
    .proyects-section {
        padding-left: 10vw;
        padding-right: 10vw;
    }
}

.proyects-title-container {
    margin-bottom: 4rem;
}

.proyects-title {
    color: var(--text-primary);
    font-size: 2.25rem;
    font-weight: 700;
    line-height: 1.25;
    letter-spacing: -0.025em;
    margin: 0;
}

@media (min-width: 768px) {
    .proyects-title {
        font-size: 3rem;
    }
}

@media (min-width: 1024px) {
    .proyects-title {
        font-size: 3.75rem;
    }
}

.text-emerald {
    color: var(--accent);
}

.proyects-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 2.5rem;
}

@media (min-width: 1280px) {
    .proyects-grid {
        grid-template-columns: repeat(2, minmax(0, 1fr));
    }
}

.project-card {
    height: 45vh;
    background-color: var(--card-bg-solid);
    border-radius: 1rem;
    overflow: hidden;
    position: relative;
    will-change: transform, opacity;
}

@media (min-width: 768px) {
    .project-card {
        height: 50vh;
    }
}

.project-img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    opacity: 0.6;
    transition: all 0.7s ease;
}

.project-card:hover .project-img {
    opacity: 1;
    transform: scale(1.05);
}

.project-overlay {
    position: absolute;
    inset: 0;
    padding: 2rem;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    background: linear-gradient(to top, rgba(15, 23, 42, 0.6) 0%, rgba(15, 23, 42, 0.1) 60%, transparent 100%);
    transition: background 0.5s ease;
}

.project-card:hover .project-overlay {
    background: linear-gradient(to top, rgba(15, 23, 42, 0.95) 0%, rgba(15, 23, 42, 0.5) 60%, transparent 100%);
}

@media (min-width: 768px) {
    .project-overlay {
        padding: 2.5rem;
    }
}

.project-content {
    transform: translateY(2rem);
    transition: transform 0.5s ease;
}

.project-card:hover .project-content {
    transform: translateY(0);
}

.project-category {
    color: var(--accent);
    font-weight: 500;
    font-size: 0.875rem;
    margin-bottom: 0.5rem;
    margin-top: 0;
}

.project-title {
    color: #f8fafc;
    font-size: 1.875rem;
    font-weight: 700;
    margin-bottom: 1.5rem;
    margin-top: 0;
}

@media (min-width: 768px) {
    .project-title {
        font-size: 2.25rem;
    }
}

.project-btn {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    color: #f8fafc;
    background: none;
    border: none;
    padding: 3px;
    cursor: pointer;
}

.project-btn-icon {
    width: 2.5rem;
    height: 2.5rem;
    border-radius: 50%;
    border: 1px solid rgba(255, 255, 255, 0.2);
    background-color: rgba(255, 255, 255, 0.05);
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s ease;
}

.project-btn:hover .project-btn-icon {
    background-color: var(--accent-hover);
    border-color: var(--accent-hover);
}

.project-btn-text {
    font-weight: 500;
    font-size: 0.875rem;
    transition: color 0.3s ease;
}

.project-btn:hover .project-btn-text {
    color: var(--accent);
}

.proyects-spacer {
    height: 20vh;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 5rem;
}
</style>