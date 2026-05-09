<template>
    <section id="about" class="about-section">
        <div ref="titleContainer" class="about-title-container">
            <p class="about-title">
                Sobre <ShinyText text="Mí" class="text-emerald" color="var(--accent)" shineColor="#B5FFE3" :speed="3" />
            </p>
        </div>

        <div ref="contentContainer" class="about-content">
            <p class="about-description">
                {{ aboutData.description }}
            </p>
        </div>
        
        <div class="about-spacer"></div>
    </section>
</template>

<script>
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import ShinyText from '../../share/ShinyText.vue';
import { aboutData } from '../../../data/about.js';

gsap.registerPlugin(ScrollTrigger);

export default {
    name: 'About',
    components: {
        ShinyText
    },
    data() {
        return {
            aboutData
        };
    },
    mounted() {
        this.initAnimations();
    },
    methods: {
        initAnimations() {
            gsap.fromTo(this.$refs.titleContainer,
                { y: 50, opacity: 0 },
                {
                    y: 0,
                    opacity: 1,
                    duration: 1,
                    ease: "power3.out",
                    scrollTrigger: {
                        trigger: this.$refs.titleContainer,
                        start: "top 80%",
                    }
                }
            );

            gsap.fromTo(this.$refs.contentContainer,
                { y: 50, opacity: 0 },
                {
                    y: 0,
                    opacity: 1,
                    duration: 1,
                    delay: 0.2,
                    ease: "power3.out",
                    scrollTrigger: {
                        trigger: this.$refs.contentContainer,
                        start: "top 85%",
                    }
                }
            );
        }
    }
}
</script>

<style scoped>
.about-section {
    position: relative;
    background-color: transparent;
    color: var(--text-primary);
    font-family: sans-serif;
    min-height: 100vh;
    padding: 6rem 5vw;
    display: flex;
    flex-direction: column;
    justify-content: center;
}

@media (min-width: 768px) {
    .about-section {
        padding-left: 10vw;
        padding-right: 10vw;
    }
}

.about-title-container {
    position: relative;
    z-index: 10;
    margin-bottom: 3rem;
    display: flex;
    justify-content: center;
    text-align: center;
}

.about-title {
    color: var(--text-primary);
    font-size: 2.25rem;
    font-weight: 700;
    line-height: 1.25;
    letter-spacing: -0.025em;
    margin: 0;
}

@media (min-width: 768px) {
    .about-title {
        font-size: 3rem;
    }
}

@media (min-width: 1024px) {
    .about-title {
        font-size: 3.75rem;
    }
}

.text-emerald {
    color: var(--accent);
}

.about-content {
    position: relative;
    z-index: 10;
    background-color: var(--card-bg);
    backdrop-filter: blur(12px);
    border: 1px solid var(--border-color);
    border-radius: 1.5rem;
    padding: 2.5rem;
    box-shadow: 0 10px 30px -5px rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
}

.about-content:hover {
    border-color: var(--border-hover);
    box-shadow: 0 10px 30px var(--hover-bg);
}

@media (min-width: 768px) {
    .about-content {
        padding: 3.5rem;
    }
}

.about-description {
    font-size: 1.125rem;
    line-height: 1.8;
    color: var(--text-secondary);
    margin: 0;
}

@media (min-width: 768px) {
    .about-description {
        font-size: 1.25rem;
    }
}

.about-spacer {
    height: 2vh;
    width: 100%;
}
</style>
