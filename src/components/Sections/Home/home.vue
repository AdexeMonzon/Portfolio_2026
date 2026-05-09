<template>
    <main class="main-container">
        <Navbar />
        

        <LightPilar class="particles-wrapper" :topColor="pillarTopColor" :bottomColor="pillarBottomColor" :intensity="0.7" :rotationSpeed="0.5"
            :glowAmount="0.010" :pillarWidth="3" :pillarHeight="0.4" :noiseIntensity="0.5"
            :pillarRotation="25" :interactive="false" :mixBlendMode="pillarMixBlendMode"
            :style="{ opacity: isLightMode ? 0.25 : 1 }" />

        <section id="home" class="hero-section">
            <div class="hero-container">
                <a href="#projects" class="hero-side-link left-link">
                    <FuzzyText :color="isLightMode ? '#000000' : '#ffffff'" fontSize="clamp(1rem, 5vw, 3.5rem)" fontFamily="'Michroma', sans-serif"
                    :hoverIntensity="0.2" :baseIntensity="0" :enableHover="true">Proyectos</FuzzyText>
                </a>

                <div class="hero-image-container">
                    <div class="glitch-wrapper">
                        <img src="/foto curri luces colores.png" alt="Adexe Monzón Santana" class="hero-image glitch-base">
                        <img src="/foto curri luces colores.png" alt="" class="hero-image glitch-layer glitch-layer-1" aria-hidden="true">
                        <img src="/foto curri luces colores.png" alt="" class="hero-image glitch-layer glitch-layer-2" aria-hidden="true">
                    </div>
                </div>

                <a href="#contact" class="hero-side-link right-link">
                    <FuzzyText :color="isLightMode ? '#000000' : '#ffffff'" fontSize="clamp(1rem, 5vw, 3.5rem)" fontFamily="'Michroma', sans-serif"
                    :hoverIntensity="0.2" :baseIntensity="0" :enableHover="true">Contactar</FuzzyText>
                </a>
            </div>
        </section>

        <div class="section-wrapper">
            <About />
        </div>
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
import ShinyText from '../../share/ShinyText.vue';
import FuzzyText from '../../share/FuzzyText.vue';
import About from '../About/index.vue';
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
        ShinyText,
        FuzzyText,
        About,
        Skills,
        Proyects,
        Studies,
        Experience,
        Contact,
        Swiper,
        LightPilar
    },
    data() {
        return {
            isLightMode: false,
            themeObserver: null
        }
    },
    computed: {
        pillarTopColor() {
            return this.isLightMode ? '#6366f1' : '#216006';
        },
        pillarBottomColor() {
            return this.isLightMode ? '#a855f7' : '#00A8F0';
        },
        pillarMixBlendMode() {
            return this.isLightMode ? 'multiply' : 'screen';
        }
    },
    mounted() {
        this.isLightMode = document.body.classList.contains('light-theme');
        this.themeObserver = new MutationObserver((mutations) => {
            mutations.forEach((mutation) => {
                if (mutation.attributeName === 'class') {
                    this.isLightMode = document.body.classList.contains('light-theme');
                }
            });
        });
        this.themeObserver.observe(document.body, { attributes: true });
        
        this.initParticles();
    },
    beforeUnmount() {
        if (this.themeObserver) {
            this.themeObserver.disconnect();
        }
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
    width: 100%;
    max-width: 100vw;
    overflow-x: hidden;
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
    padding: 3rem 0 1rem 0;
    overflow: hidden;
}

@media (min-width: 768px) {
    .hero-section {
        padding: 6rem 0 3rem 0;
    }
}

.hero-container {
    width: 100%;
    max-width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    text-align: center;
    gap: 1.5rem;
    position: relative;
    padding: 2rem 0;
}

@media (min-width: 1024px) {
    .hero-container {
        flex-direction: row;
        padding: 0 1vw;
        min-height: 60vh;
    }
}

.hero-side-link {
    z-index: 20;
    font-size: 3rem;
    font-weight: 700;
    text-decoration: none;
    transition: transform 0.3s ease;
    display: flex;
    letter-spacing: -0.02em;
}

@media (min-width: 768px) {
    .hero-side-link {
        font-size: 4rem;
    }
}

@media (min-width: 1024px) {
    .hero-side-link {
        font-size: 5rem;
    }
}

.hero-side-link:hover {
    transform: scale(1.05);
}

.text-primary {
    color: var(--text-primary);
}

.hero-image-container {
    flex: 1;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    z-index: 10;
}

@media (min-width: 1024px) {
    .hero-image-container {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        width: 100%;
        max-width: 45rem;
    }
}

.hero-image {
    width: 100%;
    max-width: 18rem;
    height: auto;
    object-fit: contain;
    transition: transform 0.5s ease, filter 0.5s ease;
    filter: drop-shadow(0 0 8px rgba(0, 0, 0, 0.3)); /* Simplified for mobile */
    -webkit-mask-image: 
    linear-gradient(to bottom, black 70%, transparent 100%),
    linear-gradient(to left, black 70%, transparent 100%),
    linear-gradient(to right, black 70%, transparent 100%);

    mask-image: 
    linear-gradient(to bottom, black 70%, transparent 100%),
    linear-gradient(to left, black 80%, transparent 100%),
    linear-gradient(to right, black 80%, transparent 100%);

    -webkit-mask-composite: source-in; 
  mask-composite: intersect;
    z-index: 10;
}

@media (min-width: 768px) {
    .hero-image {
        max-width: 24rem;
        filter: drop-shadow(0 0 8px rgba(0, 0, 0, 0.5)) drop-shadow(0 20px 30px rgba(0, 0, 0, 0.4));
    }
    .hero-image {
        max-width: 24rem;
    }
}

@media (min-width: 1024px) {
    .hero-image {
        max-width: 35rem;
    }
}

.glitch-wrapper {
    position: relative;
    display: inline-flex;
    justify-content: center;
    transition: transform 0.5s ease;
}

.glitch-wrapper:hover {
    transform: translateY(-0.3rem) scale(1.01);
}

.glitch-base {
    position: relative;
    z-index: 10;
}

.glitch-layer {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 11;
    pointer-events: none;
    opacity: 0.8;
    mix-blend-mode: hard-light;
    clip-path: polygon(0 0, 0 0, 0 0, 0 0);
}

.glitch-layer-1 {
    filter: drop-shadow(-5px 0 0 var(--accent)) drop-shadow(5px 0 0 magenta);
    animation: glitch-anim-1 2.5s infinite linear alternate-reverse;
}

.glitch-layer-2 {
    filter: drop-shadow(5px 0 0 cyan) drop-shadow(-5px 0 0 red);
    animation: glitch-anim-2 2s infinite linear alternate-reverse;
}

@keyframes glitch-anim-1 {
  0%, 80% { clip-path: polygon(0 0, 0 0, 0 0, 0 0); transform: translate(0); }
  83% { clip-path: polygon(0 10%, 100% 10%, 100% 20%, 0 20%); transform: translate(-10px); }
  88% { clip-path: polygon(0 40%, 100% 40%, 100% 50%, 0 50%); transform: translate(10px); }
  94% { clip-path: polygon(0 80%, 100% 80%, 100% 90%, 0 90%); transform: translate(-10px); }
  98%, 100% { clip-path: polygon(0 0, 0 0, 0 0, 0 0); transform: translate(0); }
}

@keyframes glitch-anim-2 {
  0%, 75% { clip-path: polygon(0 0, 0 0, 0 0, 0 0); transform: translate(0); }
  80% { clip-path: polygon(0 25%, 100% 25%, 100% 35%, 0 35%); transform: translate(10px); }
  86% { clip-path: polygon(0 55%, 100% 55%, 100% 65%, 0 65%); transform: translate(-10px); }
  92% { clip-path: polygon(0 75%, 100% 75%, 100% 85%, 0 85%); transform: translate(10px); }
  96%, 100% { clip-path: polygon(0 0, 0 0, 0 0, 0 0); transform: translate(0); }
}

.glitch-wrapper:hover .hero-image {
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
