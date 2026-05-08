<template>
  <section id="studies" class="study-section">

    <div ref="titleContainer" class="study-title-container">
      <p class="study-title">
        Mis <br> <span class="text-emerald">Estudios</span>
      </p>
    </div>

    <div class="study-container">

      <div v-for="(study, index) in studies" :key="index" ref="studyCards" class="study-card group">
        <div class="timeline-dot"></div>

        <div class="study-content">
          <div class="study-content-inner">
            <div class="study-text">
              <div class="study-period">
                {{ study.period }}
              </div>
              <h3 class="study-role">{{ study.title }}</h3>
              <h4 class="study-company">{{ study.subtitle }}</h4>
              <p class="study-description">
                {{ study.description }}
              </p>
            </div>

            <div class="study-icon-wrapper">
              <svg class="study-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 14l9-5-9-5-9 5 9 5z">
                </path>
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                  d="M12 14l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14z">
                </path>
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                  d="M12 14l9-5-9-5-9 5 9 5zm0 0l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14zm-4 6v-7.5l4-2.222">
                </path>
              </svg>
            </div>
          </div>
        </div>
      </div>

    </div>

    <div class="study-spacer"></div>
  </section>
</template>

<script>
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { studiesData } from '../../../data/studies.js';

gsap.registerPlugin(ScrollTrigger);

export default {
  name: 'Studies',
  data() {
    return {
      studies: studiesData
    }
  },
  mounted() {
    this.initAnimations();
  },
  unmounted() {
    ScrollTrigger.getAll().forEach(trigger => {
      if (trigger.vars.trigger === "#studies" ||
        (trigger.vars.trigger instanceof Element && this.$el.contains(trigger.vars.trigger))) {
        trigger.kill();
      }
    });
  },
  methods: {
    initAnimations() {
      gsap.fromTo(this.$refs.titleContainer,
        { y: 150, opacity: 0 },
        {
          y: 0,
          opacity: 1,
          ease: "power3.out",
          duration: 0.8,
          scrollTrigger: {
            trigger: "#studies",
            start: "top 80%",
          }
        }
      );

      if (this.$refs.studyCards) {
        this.$refs.studyCards.forEach((card) => {
          const dot = card.querySelector('.timeline-dot');
          if (dot) {
            gsap.fromTo(dot,
              { scale: 0, opacity: 0 },
              {
                scale: 1,
                opacity: 1,
                ease: "back.out(2)",
                duration: 0.6,
                scrollTrigger: {
                  trigger: card,
                  start: "top bottom",
                }
              }
            );
          }

          const content = card.querySelector('.study-content');
          if (content) {
            gsap.fromTo(content,
              {
                x: 100,
                opacity: 0,
              },
              {
                x: 0,
                opacity: 1,
                ease: "power3.out",
                duration: 0.6,
                delay: 0.2,
                scrollTrigger: {
                  trigger: card,
                  start: "top bottom",
                }
              }
            );
          }
        });
      }
    }
  }
}
</script>

<style scoped>
.study-section {
  position: relative;
  background-color: transparent;
  color: var(--text-primary);
  font-family: sans-serif;
  min-height: 100vh;
  padding: 8rem 5vw;
}

@media (min-width: 768px) {
  .study-section {
    padding-left: 10vw;
    padding-right: 10vw;
  }
}

.study-title-container {
  position: relative;
  z-index: 10;
  margin-bottom: 4rem;
}

.study-title {
  color: var(--text-primary);
  font-size: 2.25rem;
  font-weight: 700;
  line-height: 1.25;
  letter-spacing: -0.025em;
  margin: 0;
}

@media (min-width: 768px) {
  .study-title {
    font-size: 3rem;
  }
}

@media (min-width: 1024px) {
  .study-title {
    font-size: 3.75rem;
  }
}

.text-emerald {
  color: var(--accent);
}

.study-container {
  position: relative;
  z-index: 10;
  padding-left: 2rem;
  margin-left: 1rem;
  margin-top: 6rem;
  border-left: 2px solid var(--border-color);
}

@media (min-width: 768px) {
  .study-container {
    padding-left: 4rem;
    margin-left: 2rem;
  }
}

.study-card {
  position: relative;
  margin-bottom: 4rem;
}

.timeline-dot {
  position: absolute;
  left: -2.4rem;
  top: 2rem;
  width: 1rem;
  height: 1rem;
  border-radius: 50%;
  background-color: var(--bg-card);
  border: 2px solid var(--accent-hover);
  z-index: 10;
  transition: all 0.3s ease;
}

@media (min-width: 768px) {
  .timeline-dot {
    left: -4.4rem;
  }
}

.study-card:hover .timeline-dot {
  transform: scale(1.25);
  background-color: var(--accent);
}

.study-content {
  background-color: var(--card-bg-solid);
  border-radius: 1rem;
  padding: 1.5rem;
  border: 1px solid var(--border-color);
  transition: all 0.3s ease;
  position: relative;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

@media (min-width: 768px) {
  .study-content {
    padding: 2rem;
    border-radius: 1.5rem;
  }
}

.study-card:hover .study-content {
  border-color: var(--hover-bg);
  box-shadow: 0 20px 25px -5px var(--hover-bg);
  transform: translateY(-0.25rem);
}

.study-content-inner {
  position: relative;
  z-index: 10;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-start;
  gap: 2rem;
}

@media (min-width: 768px) {
  .study-content-inner {
    flex-direction: row;
    align-items: center;
  }
}

.study-text {
  flex: 1;
}

.study-period {
  display: inline-block;
  padding: 0.25rem 0.75rem;
  background-color: var(--hover-bg);
  color: var(--accent);
  border-radius: 9999px;
  font-weight: 500;
  font-size: 0.75rem;
  margin-bottom: 1rem;
  border: 1px solid var(--hover-bg);
}

.study-role {
  color: var(--text-primary);
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  margin-top: 0;
}

@media (min-width: 768px) {
  .study-role {
    font-size: 1.875rem;
  }
}

@media (min-width: 1024px) {
  .study-role {
    font-size: 2.25rem;
  }
}

.study-company {
  color: var(--text-muted);
  font-size: 1rem;
  font-weight: 500;
  margin: 0;
}

@media (min-width: 768px) {
  .study-company {
    font-size: 1.125rem;
  }
}

.study-description {
  color: var(--text-secondary);
  margin-top: 1rem;
  max-width: 42rem;
  font-size: 0.875rem;
  line-height: 1.625;
}

@media (min-width: 768px) {
  .study-description {
    font-size: 1rem;
  }
}

.study-icon-wrapper {
  display: none;
  flex-shrink: 0;
  align-items: center;
  justify-content: center;
  width: 5rem;
  height: 5rem;
  background-color: var(--icon-bg);
  border-radius: 1rem;
  border: 1px solid var(--border-color);
  color: var(--accent-hover);
  transition: all 0.5s ease;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
}

@media (min-width: 768px) {
  .study-icon-wrapper {
    display: flex;
  }
}

.study-card:hover .study-icon-wrapper {
  color: var(--accent);
  border-color: var(--hover-bg);
  transform: rotate(12deg);
  background-color: var(--hover-bg);
}

.study-icon {
  width: 2.5rem;
  height: 2.5rem;
}

.study-spacer {
  height: 30vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  border-top: 1px solid var(--border-color);
  margin-top: 8rem;
}
</style>
