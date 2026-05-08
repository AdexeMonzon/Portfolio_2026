<template>
    <div class="nav-wrapper scrolled-wrapper">
        <GlassSurface
            ref="navContainer"
            width="90%"
            height="64px"
            :borderRadius="10"
            :blur="16"
            :backgroundOpacity="0.6"
            :borderWidth="0.1"
            class="pointer-events-auto transition-all duration-500 ease-in-out font-sans"
            style="max-width: 72rem;"
        >
            <div class="flex justify-between items-center w-full px-4 md:px-8">
                <div class="nav-logo group">
                    <div class="nav-logo-dot"></div>
                    <span class="nav-logo-text">Adexe Monzón</span>
                </div>

                <div class="nav-links">
                    <a href="#home" class="nav-item">Inicio</a>
                    <a href="#skills" class="nav-item">Tecnologías</a>
                    <a href="#projects" class="nav-item">Proyectos</a>
                    <a href="#studies" class="nav-item">Estudios</a>
                    <a href="#experience" class="nav-item">Experiencia</a>
                    <a href="#contact" class="nav-item">Contacto</a>
                    <button @click="toggleTheme" class="theme-toggle" aria-label="Cambiar tema">
                        <svg v-if="isDark" class="theme-icon" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
                        </svg>
                        <svg v-else class="theme-icon" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
                        </svg>
                    </button>
                </div>

                <div class="nav-spacer"></div>
            </div>
        </GlassSurface>
    </div>
</template>

<script>
import { gsap } from 'gsap';
import GlassSurface from './GlassSurface.vue';

export default {
    name: 'Navbar',
    components: {
        GlassSurface
    },

    data() {
        return {
            isDark: true
        };
    },

    mounted() {
        this.initAnimation();
        
        const savedTheme = localStorage.getItem('theme');
        if (savedTheme === 'light') {
            this.isDark = false;
            document.body.classList.add('light-theme');
        }
    },

    unmounted() {
    },

    methods: {
        toggleTheme() {
            this.isDark = !this.isDark;
            if (this.isDark) {
                document.body.classList.remove('light-theme');
                localStorage.setItem('theme', 'dark');
            } else {
                document.body.classList.add('light-theme');
                localStorage.setItem('theme', 'light');
            }
        },

        initAnimation() {
            const tl = gsap.timeline();
            const navElement = this.$refs.navContainer.$el || this.$refs.navContainer;

            tl.from(navElement, {
                y: -100,
                opacity: 0,
                duration: 1,
                ease: 'expo.out',
            })
                .fromTo('.nav-item',
                    { y: -20, opacity: 0 },
                    {
                        y: 0,
                        opacity: 1,
                        duration: 0.6,
                        stagger: 0.1,
                        ease: 'back.out(1.7)',
                    },
                    "-=0.7");
        }
    }
};
</script>

<style scoped>
.nav-wrapper {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 50;
    display: flex;
    justify-content: center;
    pointer-events: none;
    transition: padding-top 0.5s ease;
    padding-top: 0;
}

.scrolled-wrapper {
    padding-top: 1rem;
}

.nav-logo {
    color: var(--text-primary);
    font-weight: 700;
    font-size: 1.125rem;
    letter-spacing: -0.025em;
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 0.75rem;
    transition: transform 0.3s ease;
    flex-shrink: 0;
    white-space: nowrap;
}

.nav-logo:hover {
    transform: scale(1.05);
}

@media (min-width: 768px) {
    .nav-logo {
        font-size: 1.25rem;
    }
}

.nav-logo-dot {
    width: 0.625rem;
    height: 0.625rem;
    border-radius: 50%;
    background-color: var(--accent);
    transition: box-shadow 0.3s ease;
}

.nav-logo:hover .nav-logo-dot {
    box-shadow: 0 0 12px var(--accent);
}

.nav-logo-text {
    background: linear-gradient(to right, var(--text-primary), var(--text-muted));
    -webkit-background-clip: text;
    color: transparent;
    background-clip: text;
}

.nav-links {
    display: none;
    align-items: center;
    gap: 0.5rem;
    transition: all 0.5s ease;
}

@media (min-width: 768px) {
    .nav-links {
        display: flex;
    }
}

.nav-item {
    color: var(--text-secondary);
    padding: 0.5rem 1.25rem;
    border-radius: 9999px;
    font-size: 0.875rem;
    font-weight: 500;
    transition: all 0.3s ease;
    text-decoration: none;
    white-space: nowrap;
    opacity: 1;
}

.nav-item:hover {
    color: var(--text-primary);
    background-color: var(--border-color);
}

.theme-toggle {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0.5rem;
    color: var(--text-secondary);
    border-radius: 50%;
    transition: all 0.3s ease;
    cursor: pointer;
    background: transparent;
    border: none;
}

.theme-toggle:hover {
    color: var(--accent);
    background-color: var(--border-color);
}

.theme-icon {
    width: 1.25rem;
    height: 1.25rem;
}

.nav-spacer {
    display: none;
    width: 6rem;
}

@media (min-width: 768px) {
    .nav-spacer {
        display: block;
    }
}
</style>