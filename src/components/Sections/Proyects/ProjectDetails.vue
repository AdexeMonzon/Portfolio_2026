<template>
    <Teleport to="body">
        <div ref="detailPanel" class="detail-panel">

            <button @click="closePanel" class="close-btn">
                <svg class="close-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12">
                    </path>
                </svg>
            </button>

            <div v-if="project" class="detail-container">

                <div class="detail-info">
                    <p class="detail-content detail-category">{{ project.category }}</p>
                    <h2 class="detail-content detail-title">{{ project.title }}</h2>
                    <p class="detail-content detail-desc">{{ project.desc }}</p>

                    <div v-if="project.icons && project.icons.length > 0" class="detail-content tech-container">
                        <h3 class="tech-title">Tecnologías</h3>
                        <div class="tech-list">
                            <div v-for="(icon, index) in project.icons" :key="index" class="icon-wrapper" v-html="icon">
                            </div>
                        </div>
                    </div>

                    <div class="detail-content links-container">

                        <a v-if="project.githubFrontend" :href="project.githubFrontend" target="_blank"
                            class="link-btn link-github">
                            <svg class="link-icon" fill="currentColor" viewBox="0 0 24 24">
                                <path fill-rule="evenodd"
                                    d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"
                                    clip-rule="evenodd"></path>
                            </svg>
                            Frontend
                        </a>

                        <a v-if="project.githubBackend" :href="project.githubBackend" target="_blank"
                            class="link-btn link-github">
                            <svg class="link-icon" fill="currentColor" viewBox="0 0 24 24">
                                <path fill-rule="evenodd"
                                    d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"
                                    clip-rule="evenodd"></path>
                            </svg>
                            Backend
                        </a>
                    </div>
                </div>

                <div class="detail-image-wrapper detail-content">
                    <div class="detail-image-container group">
                        <Swiper :images="project.images" class="detail-image" />
                    </div>
                </div>

            </div>
        </div>
    </Teleport>
</template>

<script>
import { gsap } from 'gsap';
import Swiper from '../../share/swiper-slider.vue';

export default {
    name: 'ProjectDetails',
    components: {
        Swiper
    },
    props: {
        project: {
            type: Object,
            default: null
        }
    },
    methods: {
        open() {
            document.body.style.overflow = 'hidden';
            const tl = gsap.timeline();
            tl.to(this.$refs.detailPanel, {
                display: 'flex',
                duration: 0
            })
                .fromTo(this.$refs.detailPanel,
                    { clipPath: 'circle(0% at 50% 50%)' },
                    { clipPath: 'circle(150% at 50% 50%)', duration: 1, ease: 'expo.inOut' }
                )
                .fromTo(this.$el.querySelectorAll('.detail-content'), {
                    y: 50,
                    opacity: 0
                }, {
                    y: 0,
                    opacity: 1,
                    stagger: 0.1,
                    duration: 0.5
                });
        },
        closePanel() {
            const tl = gsap.timeline({
                onComplete: () => {
                    document.body.style.overflow = 'auto';
                    gsap.set(this.$refs.detailPanel, { display: 'none' });
                    this.$emit('closed');
                }
            });

            tl.to(this.$refs.detailPanel, {
                clipPath: 'circle(0% at 50% 50%)',
                duration: 0.8,
                ease: 'expo.inOut'
            });
        }
    }
}
</script>

<style scoped>


.detail-panel {
    position: fixed;
    inset: 0;
    z-index: 9999;
    display: none;
    /* handled by GSAP */
    background-color: var(--bg-glass);
    backdrop-filter: blur(4px);
    flex-direction: column;
    align-items: center;
    justify-content: flex-start;
    padding: 1.5rem;
    overflow-y: auto;
    font-family: sans-serif;
    clip-path: circle(0% at 50% 50%);
}

@media (min-width: 768px) {
    .detail-panel {
        padding: 3rem;
    }
}

.close-btn {
    position: fixed;
    top: 1.5rem;
    right: 1.5rem;
    color: var(--text-muted);
    background-color: var(--bg-secondary);
    border: 1px solid var(--border-color);
    border-radius: 50%;
    width: 3rem;
    height: 3rem;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s ease;
    z-index: 50;
    cursor: pointer;
}

@media (min-width: 768px) {
    .close-btn {
        top: 2.5rem;
        right: 2.5rem;
    }
}

.close-btn:hover {
    background-color: var(--bg-card);
    color: var(--text-primary);
}

.close-icon {
    width: 1.5rem;
    height: 1.5rem;
}

.detail-container {
    max-width: 72rem;
    width: 100%;
    display: flex;
    flex-direction: column-reverse;
    gap: 2rem;
    align-items: center;
    margin-top: 5rem;
    margin-bottom: 3rem;
}

@media (min-width: 1024px) {
    .detail-container {
        flex-direction: row;
        gap: 5rem;
        margin-top: 6rem;
    }
}

.detail-info {
    flex: 1;
    text-align: left;
    position: relative;
    z-index: 10;
    width: 100%;
}

.detail-category {
    color: var(--accent);
    font-weight: 500;
    font-size: 0.875rem;
    margin-bottom: 0.5rem;
    text-transform: uppercase;
    letter-spacing: 0.025em;
}

.detail-title {
    color: var(--text-primary);
    font-size: 1.875rem;
    font-weight: 700;
    margin-bottom: 1.5rem;
    line-height: 1.25;
}

@media (min-width: 768px) {
    .detail-title {
        font-size: 3rem;
    }
}

.detail-desc {
    color: var(--text-secondary);
    font-size: 1rem;
    margin-bottom: 2.5rem;
    line-height: 1.625;
}

@media (min-width: 768px) {
    .detail-desc {
        font-size: 1.125rem;
    }
}

.tech-container {
    margin-bottom: 2.5rem;
}

.tech-title {
    font-size: 0.875rem;
    color: var(--text-muted);
    font-weight: 500;
    margin-bottom: 1rem;
}

.tech-list {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
}

.icon-wrapper {
    width: 2.5rem;
    height: 2.5rem;
    background-color: var(--bg-secondary);
    border-radius: 0.75rem;
    border: 1px solid var(--border-color);
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0.5rem;
    transition: all 0.3s ease;
}

@media (min-width: 768px) {
    .icon-wrapper {
        width: 3rem;
        height: 3rem;
    }
}

.icon-wrapper:hover {
    transform: translateY(-0.25rem);
    border-color: var(--border-hover);
    box-shadow: 0 10px 15px -3px var(--border-hover);
}

.links-container {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
}

.link-btn {
    border-radius: 0.5rem;
    padding: 0.75rem 1.5rem;
    font-weight: 500;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    text-decoration: none;
}

.link-btn:hover {
    transform: translateY(-0.25rem);
}

.link-web {
    background-color: var(--accent-hover);
    color: var(--bg-primary);
}

.link-web:hover {
    background-color: var(--accent);
}

.link-github {
    background-color: var(--bg-card);
    color: var(--text-primary);
    border: 1px solid var(--border-color);
}

.link-github:hover {
    background-color: #334155;
}

.link-icon {
    width: 1rem;
    height: 1rem;
}

.detail-image-wrapper {
    flex: 1;
    width: 100%;
    display: flex;
    justify-content: center;
    position: relative;
    z-index: 10;
}

@media (min-width: 1024px) {
    .detail-image-wrapper {
        justify-content: flex-end;
    }
}

.detail-image-container {
    position: relative;
    width: 100%;
    max-width: 100%;
    border-radius: 1rem;
    overflow: hidden;
    background-color: var(--bg-secondary);
    border: 1px solid var(--border-color);
    box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
}

@media (min-width: 1024px) {
    .detail-image-container {
        max-width: 32rem;
    }
}

.detail-image {
    width: 100%;
    height: auto;
    object-fit: cover;
    opacity: 0.9;
    transition: opacity 0.5s ease;
}

.detail-image-container:hover .detail-image {
    opacity: 1;
}
</style>

<style lang="scss">
.icon-wrapper {

    img,
    svg {
        width: 100%;
        height: 100%;
        object-fit: contain;
    }
}
</style>
