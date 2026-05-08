<template>
    <main class="main-container">
        <Navbar />
        

        <LightPilar class="particles-wrapper" topColor="#216006" bottomColor="#00A8F0" :intensity="0.7" :rotationSpeed="0.3"
            :glowAmount="0.002" :pillarWidth="3" :pillarHeight="0.4" :noiseIntensity="0.5"
            :pillarRotation="25" :interactive="false" mixBlendMode="screen" />

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
import LightPilar from '../../share/LightPilar.vue';
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
        Swiper,
        LightPilar
    },
    mounted() {
        this.initParticles();
    },
    methods: {
        initParticles() {
        }
    }
}
</script>

<style scoped>
.main-container {
    color: var(--text-primary);
    font-family: sans-serif;
}

.particles-wrapper {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 0;
    overflow: hidden;
    filter: blur(11px);
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
    filter: drop-shadow(0 0 8px rgba(0, 0, 0, 0.5)) drop-shadow(0 20px 30px rgba(0, 0, 0, 0.4));
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
