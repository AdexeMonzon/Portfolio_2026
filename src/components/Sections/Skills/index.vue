<template>
  <section id="skills" class="skills-section">

    <div class="skills-title-container title-container-skills">
      <p class="skills-title">
        <ShinyText text="Tecnologías" class="text-emerald" color="var(--accent)" shineColor="#B5FFE3" :speed="3" />
      </p>
      <div class="skills-line"></div>
    </div>

    <div class="skills-grid-container">
      <div v-for="(tech, index) in technologies" :key="index" class="tech-card">

        <div class="tech-icon-wrapper">
          <img v-if="tech.icon.startsWith('http')" :src="tech.icon" :alt="tech.name" class="tech-icon-img">
          <img v-else :src="tech.icon" :alt="tech.name" class="tech-icon-svg">
        </div>

        <p class="tech-name">
          {{ tech.name }}
        </p>

      </div>
    </div>
  </section>
</template>

<script>
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { technologies } from '../../../data/technologies.js';
import ShinyText from '../../share/ShinyText.vue';

gsap.registerPlugin(ScrollTrigger);

export default {
  name: 'SkillsView',
  components: {
    ShinyText
  },
  data() {
    return {
      technologies
    }
  },
  mounted() {
    this.initAnimations();
  },
  methods: {
    initAnimations() {
      gsap.fromTo(".title-container-skills p",
        { y: 50, opacity: 0 },
        {
          y: 0,
          opacity: 1,
          duration: 1,
          ease: "power3.out",
          scrollTrigger: {
            trigger: "#skills",
            start: "top 85%",
          }
        }
      );

      gsap.fromTo(".skills-line",
        { scaleX: 0 },
        {
          scaleX: 1,
          duration: 1,
          delay: 0.2,
          ease: "power3.out",
          scrollTrigger: {
            trigger: "#skills",
            start: "top 85%",
          }
        }
      );

      gsap.fromTo(".tech-card",
        { y: 50, opacity: 0, scale: 0.9 },
        {
          y: 0,
          opacity: 1,
          scale: 1,
          duration: 0.6,
          stagger: 0.05,
          ease: "back.out(1.5)",
          scrollTrigger: {
            trigger: ".tech-card",
            start: "top 85%",
          }
        }
      );
    }
  }
}
</script>

<style scoped>
.skills-section {
  position: relative;
  background-color: transparent;
  color: var(--text-primary);
  font-family: sans-serif;
  padding: 6rem 5vw;
}

@media (min-width: 768px) {
  .skills-section {
    padding: 6rem 10vw;
  }
}

.skills-title-container {
  position: relative;
  z-index: 10;
  margin-bottom: 4rem;
}

.skills-title {
  color: var(--text-primary);
  font-size: 2.25rem;
  font-weight: 700;
  line-height: 1.25;
  letter-spacing: -0.025em;
  margin: 0;
}

@media (min-width: 768px) {
  .skills-title {
    font-size: 3rem;
  }
}

@media (min-width: 1024px) {
  .skills-title {
    font-size: 3.75rem;
  }
}

.skills-line {
  height: 0.25rem;
  width: 6rem;
  background-color: var(--accent-hover);
  margin-top: 1.5rem;
  border-radius: 9999px;
  transform-origin: left;
}

.skills-grid-container {
  position: relative;
  z-index: 10;
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1.5rem;
  width: 100%;
  max-width: 72rem;
  margin: 0 auto;
}

@media (min-width: 640px) {
  .skills-grid-container {
    grid-template-columns: repeat(3, minmax(0, 1fr));
  }
}

@media (min-width: 768px) {
  .skills-grid-container {
    grid-template-columns: repeat(4, minmax(0, 1fr));
  }
}

@media (min-width: 1024px) {
  .skills-grid-container {
    grid-template-columns: repeat(5, minmax(0, 1fr));
  }
}

.tech-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 1.5rem;
  border-radius: 1.5rem;
  background-color: var(--bg-nav);
  backdrop-filter: blur(12px);
  border: 1px solid var(--border-color);
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
  transition: all 0.3s ease;
}

.tech-card:hover {
  border-color: var(--border-hover);
  background-color: var(--hover-bg);
  box-shadow: 0 0 20px var(--hover-bg);
}

.tech-icon-wrapper {
  width: 4rem;
  height: 4rem;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1rem;
  transition: all 0.3s ease;
}

.tech-card:hover .tech-icon-wrapper {
  transform: translateY(-0.5rem) scale(1.1);
}

.tech-icon-img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
  filter: drop-shadow(0 4px 3px rgba(0, 0, 0, 0.07)) drop-shadow(0 2px 2px rgba(0, 0, 0, 0.06));
}

.tech-icon-svg {
  width: 3rem;
  height: 3rem;
  object-fit: contain;
  filter: drop-shadow(0 4px 3px rgba(0, 0, 0, 0.07)) drop-shadow(0 2px 2px rgba(0, 0, 0, 0.06));
  opacity: 0.8;
  transition: opacity 0.3s ease;
}

.tech-card:hover .tech-icon-svg {
  opacity: 1;
}

.tech-name {
  color: var(--text-secondary);
  font-weight: 500;
  font-size: 0.875rem;
  text-align: center;
  transition: color 0.3s ease;
  margin: 0;
}

@media (min-width: 768px) {
  .tech-name {
    font-size: 1rem;
  }
}

.tech-card:hover .tech-name {
  color: var(--accent);
}

.tech-card img[alt="AWS (EC2)"] {
  filter: drop-shadow(0 0 2px rgba(255, 255, 255, 0.8));
  background: rgba(255, 255, 255, 0.9);
  padding: 4px;
  border-radius: 8px;
}
</style>
