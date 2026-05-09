<template>
    <section id="experience" class="experience-section">

        <div ref="titleContainer" class="experience-title-container">
            <p class="experience-title">
                Mi <br> <ShinyText text="Experiencia" class="text-emerald" color="var(--accent)" shineColor="#B5FFE3" :speed="3" />
            </p>
        </div>

        <div class="experience-container">
            <div class="timeline-line-bg">
                <div ref="timelineLine" class="timeline-line-progress"></div>
            </div>

            <div v-for="(exp, index) in experience" :key="index" ref="experienceCards" class="experience-card group">
                <div class="timeline-dot"></div>

                <div class="experience-content">
                    <div class="experience-content-inner" @click="toggleDropdown(index)" style="cursor: pointer;">
                        <div class="experience-text">
                            <div class="experience-period">
                                {{ exp.period }}
                            </div>
                            <h3 class="experience-role">{{ exp.role }}</h3>
                            <h4 class="experience-company">{{ exp.company }} — {{ exp.location }}</h4>

                            <div class="experience-dropdown" :class="{ 'is-open': activeDropdown === index }">
                                <div class="experience-dropdown-inner">
                                    <p class="experience-desc">{{ exp.description }}</p>
                                    <ul class="experience-tasks">
                                        <li v-for="(task, tIndex) in exp.tasks" :key="tIndex">{{ task }}</li>
                                    </ul>
                                </div>
                            </div>
                        </div>

                        <div class="experience-icon-wrapper" :class="{ 'icon-rotated': activeDropdown === index }">
                            <svg class="experience-icon chevron-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24"
                                xmlns="http://www.w3.org/2000/svg">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                            </svg>
                        </div>
                    </div>
                </div>
            </div>

        </div>

        <div class="experience-spacer"></div>
    </section>
</template>

<script>
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { experienceData } from '../../../data/experience.js';
import ShinyText from '../../share/ShinyText.vue';

gsap.registerPlugin(ScrollTrigger);

export default {
    name: 'Experience',
    components: {
        ShinyText
    },
    data() {
        return {
            experience: experienceData,
            activeDropdown: null
        }
    },
    mounted() {
        this.initAnimations();
    },
    unmounted() {
        ScrollTrigger.getAll().forEach(trigger => {
            if (trigger.vars.trigger === "#experience" ||
                (trigger.vars.trigger instanceof Element && this.$el.contains(trigger.vars.trigger))) {
                trigger.kill();
            }
        });
    },
    methods: {
        toggleDropdown(index) {
            this.activeDropdown = this.activeDropdown === index ? null : index;
            setTimeout(() => {
                ScrollTrigger.refresh();
            }, 400);
        },
        initAnimations() {
            gsap.fromTo(this.$refs.titleContainer,
                { y: 150, opacity: 0, rotateX: -20, transformPerspective: 500 },
                {
                    y: 0,
                    opacity: 1,
                    rotateX: 0,
                    ease: "power3.out",
                    duration: 1,
                    scrollTrigger: {
                        trigger: "#experience",
                        start: "top 80%",
                    }
                }
            );

            if (this.$refs.timelineLine) {
                gsap.to(this.$refs.timelineLine, {
                    scaleY: 1,
                    ease: "none",
                    scrollTrigger: {
                        trigger: ".experience-container",
                        start: "top 90%",
                        end: "bottom 90%",
                        scrub: 1
                    }
                });
            }

            if (this.$refs.experienceCards) {
                this.$refs.experienceCards.forEach((card) => {
                    const dot = card.querySelector('.timeline-dot');
                    if (dot) {
                        gsap.fromTo(dot,
                            { scale: 0, opacity: 0 },
                            {
                                scale: 1,
                                opacity: 1,
                                ease: "elastic.out(1, 0.5)",
                                duration: 0.8,
                                scrollTrigger: {
                                    trigger: card,
                                    start: "top bottom+=50",
                                }
                            }
                        );
                    }

                    const content = card.querySelector('.experience-content');
                    if (content) {
                        gsap.fromTo(content,
                            {
                                y: 80,
                                opacity: 0,
                                rotateX: -30,
                                scale: 0.9,
                                filter: "blur(15px)",
                                transformPerspective: 800
                            },
                            {
                                y: 0,
                                opacity: 1,
                                rotateX: 0,
                                scale: 1,
                                filter: "blur(0px)",
                                ease: "power3.out",
                                duration: 0.8,
                                scrollTrigger: {
                                    trigger: card,
                                    start: "top bottom+=50",
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
.experience-section {
    position: relative;
    background-color: transparent;
    color: var(--text-primary);
    font-family: sans-serif;
    min-height: 100vh;
    padding: 8rem 5vw;
}

@media (min-width: 768px) {
    .experience-section {
        padding-left: 10vw;
        padding-right: 10vw;
    }
}

.experience-title-container {
    position: relative;
    z-index: 10;
    margin-bottom: 4rem;
}

.experience-title {
    color: var(--text-primary);
    font-size: 2.25rem;
    font-weight: 700;
    line-height: 1.25;
    letter-spacing: -0.025em;
    margin: 0;
}

@media (min-width: 768px) {
    .experience-title {
        font-size: 3rem;
    }
}

@media (min-width: 1024px) {
    .experience-title {
        font-size: 3.75rem;
    }
}

.text-emerald {
    color: var(--accent);
}

.experience-container {
    position: relative;
    z-index: 10;
    padding-left: 2rem;
    margin-left: 1rem;
    margin-top: 6rem;
}

@media (min-width: 768px) {
    .experience-container {
        padding-left: 4rem;
        margin-left: 2rem;
    }
}

.timeline-line-bg {
    position: absolute;
    left: -1px;
    top: 0;
    bottom: 0;
    width: 2px;
    background-color: var(--border-color);
    border-radius: 9999px;
}

.timeline-line-progress {
    width: 100%;
    height: 100%;
    background-color: var(--accent-hover);
    transform-origin: top;
    transform: scaleY(0);
    border-radius: 9999px;
}

.experience-card {
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

.experience-card:hover .timeline-dot {
    transform: scale(1.25);
    background-color: var(--accent);
}

.experience-content {
    background-color: var(--bg-nav);
    backdrop-filter: blur(12px);
    border-radius: 1rem;
    padding: 1.5rem;
    border: 1px solid var(--border-color);
    transition: all 0.3s ease;
    position: relative;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

@media (min-width: 768px) {
    .experience-content {
        padding: 2rem;
        border-radius: 1.5rem;
    }
}

.experience-card:hover .experience-content {
    border-color: var(--hover-bg);
    box-shadow: 0 20px 25px -5px var(--hover-bg);
    transform: translateY(-0.25rem);
}

.experience-content-inner {
    position: relative;
    z-index: 10;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-start;
    gap: 2rem;
}

@media (min-width: 768px) {
    .experience-content-inner {
        flex-direction: row;
        align-items: center;
    }
}

.experience-text {
    flex: 1;
}

.experience-period {
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

.experience-role {
    color: var(--text-primary);
    font-size: 1.5rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
    margin-top: 0;
}

@media (min-width: 768px) {
    .experience-role {
        font-size: 1.875rem;
    }
}

@media (min-width: 1024px) {
    .experience-role {
        font-size: 2.25rem;
    }
}

.experience-company {
    color: var(--text-muted);
    font-size: 1rem;
    font-weight: 500;
    margin: 0;
}

@media (min-width: 768px) {
    .experience-company {
        font-size: 1.125rem;
    }
}

.experience-icon-wrapper {
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
    .experience-icon-wrapper {
        display: flex;
    }
}

.experience-icon-wrapper.icon-rotated {
    transform: rotate(180deg);
    background-color: var(--hover-bg);
    color: var(--accent);
    border-color: var(--hover-bg);
}

.experience-card:hover .experience-icon-wrapper:not(.icon-rotated) {
    color: var(--accent);
    border-color: var(--hover-bg);
    transform: translateY(-0.25rem);
    background-color: var(--hover-bg);
}

.experience-icon {
    width: 2.5rem;
    height: 2.5rem;
    transition: transform 0.3s ease;
}

.experience-dropdown {
    display: grid;
    grid-template-rows: 0fr;
    transition: grid-template-rows 0.4s ease-out;
    width: 100%;
}

.experience-dropdown.is-open {
    grid-template-rows: 1fr;
}

.experience-dropdown-inner {
    overflow: hidden;
}

.experience-desc {
    color: var(--text-secondary);
    margin-top: 1.5rem;
    font-size: 0.95rem;
    line-height: 1.6;
}

.experience-tasks {
    margin-top: 1rem;
    padding-left: 1.5rem;
    color: var(--text-muted);
    font-size: 0.9rem;
    line-height: 1.6;
    margin-bottom: 0.5rem;
}

.experience-tasks li {
    margin-bottom: 0.5rem;
    list-style-type: disc;
}

.experience-tasks li::marker {
    color: var(--accent);
}

.experience-spacer {
    height: 10vh;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    border-top: 1px solid var(--border-color);
    margin-top: 8rem;
}
</style>
