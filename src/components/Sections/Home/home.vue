<template>
    <main class="main-container">
        <Navbar />

        <div class="particles-wrapper">
            <div class="particles-glow"></div>

            <div v-for="n in 70" :key="n" class="particle particle-item"></div>
        </div>

        <section id="home" class="hero-section">
            <div class="hero-container">
                <div class="hero-text-container">
                    <h1 class="hero-title">
                        <span class="hero-title-greeting">Hola, soy</span>
                        <span class="hero-title-name">Adexe Monzón</span>
                    </h1>

                    <div class="hero-description">
                        <p>
                            Técnico en <strong class="hero-highlight">Desarrollo de Aplicaciones Web</strong> con una
                            gran pasión por la creación de software.
                        </p>
                        <p class="hero-subdescription">
                            Mi objetivo principal es aportar valor a las empresas mediante soluciones de calidad.
                            Destaco por mi <span class="hero-subhighlight">responsabilidad, ambición y capacidad de
                                trabajo en equipo</span>, contribuyendo activamente al éxito de cada proyecto.
                        </p>
                    </div>
                </div>

                <div class="hero-image-container">
                    <img src="/foto curri luces colores.png" alt="Adexe Monzón Santana" class="hero-image">
                </div>
            </div>
        </section>

        <div class="section-wrapper">
            <Proyects />
        </div>
        <div class="section-wrapper">
            <Skills />
        </div>
        <div class="section-wrapper">
            <Experience />
        </div>
        <div class="section-wrapper">
            <Studies />
        </div>
        <div class="section-wrapper padding-bottom-large">
            <Contact />
        </div>

    </main>
</template>

<script>
import Navbar from '../../share/nav-component.vue';
import Proyects from '../Proyects/index.vue';
import Studies from '../Studies/index.vue';
import Experience from '../Experience/index.vue';
import Contact from '../Contact/index.vue';
import Skills from '../Skills/index.vue';
import Swiper from '../../share/swiper-slider.vue';
import { gsap } from 'gsap';

export default {
    name: 'Home',
    components: {
        Navbar,
        Skills,
        Proyects,
        Studies,
        Experience,
        Contact,
        Swiper
    },
    mounted() {
        this.initParticles();
    },
    methods: {
        initParticles() {
            const particles = document.querySelectorAll('.particle');

            particles.forEach((p) => {
                gsap.set(p, {
                    x: "random(0, " + window.innerWidth + ")",
                    y: "random(0, " + window.innerHeight + ")",
                    scale: "random(0.5, 2.5)",
                    opacity: "random(0.1, 0.6)",
                    width: "random(3, 8)",
                    height: "random(3, 8)",
                });

                gsap.to(p, {
                    x: "+=random(-100, 100)",
                    y: "+=random(-100, 100)",
                    opacity: "random(0.1, 0.8)",
                    duration: "random(4, 12)",
                    repeat: -1,
                    yoyo: true,
                    ease: "sine.inOut"
                });
            });
        }
    }
}
</script>

<style scoped>
.main-container {
    background-color: var(--bg-primary);
    color: var(--text-primary);
    font-family: sans-serif;
    transition: background-color 0.5s ease, color 0.5s ease;
}

.particles-wrapper {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 0;
    background-color: var(--bg-primary);
    overflow: hidden;
    transition: background-color 0.5s ease;
}

.particles-glow {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 80vw;
    height: 80vw;
    opacity: 0.1;
    filter: blur(150px);
    border-radius: 50%;
}

.particle-item {
    position: absolute;
    border-radius: 50%;
    background-color: var(--accent);
    filter: blur(2px);
    opacity: 0.6;
    box-shadow: 0 0 10px var(--accent);
}

@media (min-width: 768px) {
    .particle-item {
        filter: blur(4px);
    }
}

.hero-section {
    position: relative;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 6rem 1.5rem 3rem 1.5rem;
    overflow: hidden;
}

@media (min-width: 768px) {
    .hero-section {
        padding-left: 3rem;
        padding-right: 3rem;
    }
}

.hero-container {
    width: 100%;
    max-width: 64rem;
    display: flex;
    flex-direction: column-reverse;
    align-items: center;
    justify-content: space-between;
    gap: 3rem;
}

@media (min-width: 1024px) {
    .hero-container {
        flex-direction: row;
    }
}

.hero-text-container {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    z-index: 10;
}

@media (min-width: 1024px) {
    .hero-text-container {
        align-items: flex-start;
        text-align: left;
    }
}

.hero-title {
    font-size: 2.25rem;
    font-weight: 700;
    letter-spacing: -0.025em;
    line-height: 1.25;
    margin: 0;
}

@media (min-width: 640px) {
    .hero-title {
        font-size: 3rem;
    }
}

@media (min-width: 768px) {
    .hero-title {
        font-size: 3.75rem;
    }
}

.hero-title-greeting {
    display: block;
    color: var(--text-secondary);
}

.hero-title-name {
    display: block;
    color: var(--accent);
    margin-top: 0.5rem;
}

.hero-description {
    margin-top: 1.5rem;
    font-size: 1.125rem;
    color: var(--text-muted);
    max-width: 32rem;
    line-height: 1.625;
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

@media (min-width: 768px) {
    .hero-description {
        font-size: 1.25rem;
    }
}

.hero-description p {
    margin: 0;
}

.hero-highlight {
    color: var(--accent);
    font-weight: 500;
}

.hero-subdescription {
    font-size: 1rem;
}

@media (min-width: 768px) {
    .hero-subdescription {
        font-size: 1.125rem;
    }
}

.hero-subhighlight {
    color: var(--text-secondary);
}

.hero-image-container {
    flex: 1;
    display: flex;
    justify-content: center;
    width: 100%;
    max-width: 28rem;
    z-index: 10;
}

@media (min-width: 1024px) {
    .hero-image-container {
        justify-content: flex-end;
    }
}

.hero-image {
    width: 100%;
    max-width: 16rem;
    height: auto;
    object-fit: contain;
    transition: transform 0.5s ease, filter 0.5s ease;
    filter: drop-shadow(0 0 8px rgba(0,0,0,0.5)) drop-shadow(0 20px 30px rgba(0, 0, 0, 0.4));
    mask-image: radial-gradient(ellipse at center, black 50%, transparent 95%);
    z-index: 10;
}

@media (min-width: 768px) {
    .hero-image {
        max-width: 22rem;
    }
}

.hero-image:hover {
    transform: translateY(-0.3rem) scale(1.01);
    filter: drop-shadow(0 15px 20px var(--border-hover));
}

.section-wrapper {
    position: relative;
    z-index: 10;
    background-color: transparent;
}

.padding-bottom-large {
    padding-bottom: 8rem;
}
</style>
