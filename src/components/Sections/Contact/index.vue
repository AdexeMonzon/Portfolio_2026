<template>
    <section id="contact" class="contact-section">

        <div class="contact-container">

            <div class="title-container-contact">
                <p class="contact-title">
                    ¿Necesitas hablarme?
                </p>
                <div class="contact-line"></div>
            </div>

            <div class="contact-info">
                <div class="contact-header">
                    <h3 class="contact-subtitle">Ponte en contacto</h3>
                    <p class="contact-desc">
                        Actualmente estoy abierto a nuevas oportunidades. Si tienes algún proyecto en mente, ¡no dudes
                        en escribirme y te responderé lo antes posible!
                    </p>
                </div>

                <div class="contact-cards">
                    <a href="mailto:adexems.projects@gmail.com" class="contact-card">
                        <div class="contact-icon-wrapper">
                            <svg class="contact-icon" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                            </svg>
                        </div>
                        <div class="contact-card-text">
                            <p class="contact-card-label">Envíame un correo</p>
                            <span class="contact-card-value">adexems.projects@gmail.com</span>
                        </div>
                    </a>

                    <a href="https://www.linkedin.com/in/adexe-monz%C3%B3n-santana-536318346/" target="_blank"
                        class="contact-card">
                        <div class="contact-icon-wrapper">
                            <svg class="contact-icon" fill="currentColor" viewBox="0 0 24 24">
                                <path
                                    d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z" />
                            </svg>
                        </div>
                        <div class="contact-card-text">
                            <p class="contact-card-label">Conecta conmigo</p>
                            <span class="contact-card-value">Adexe Monzón</span>
                        </div>
                    </a>
                </div>
            </div>

            <div class="contact-form-wrapper">
                <form class="contact-form">
                    <div class="form-glow"></div>

                    <div class="form-row">
                        <div class="form-group">
                            <label>Nombre</label>
                            <input type="text" class="form-input" placeholder="Tu nombre">
                        </div>

                        <div class="form-group">
                            <label>Email</label>
                            <input type="email" class="form-input" placeholder="tu@email.com">
                        </div>
                    </div>

                    <div class="form-group">
                        <label>Asunto</label>
                        <input type="text" class="form-input" placeholder="¿De qué trata el mensaje?">
                    </div>

                    <div class="form-group">
                        <label>Mensaje</label>
                        <textarea rows="4" class="form-input form-textarea" placeholder="Cuéntame más..."></textarea>
                    </div>

                    <button type="button" class="form-submit">
                        Enviar mensaje
                    </button>
                </form>
            </div>
        </div>
    </section>
</template>

<script>
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

export default {
    name: 'ContactView',
    mounted() {
        this.initAnimations();
    },
    methods: {
        //animaciones de gsap
        initAnimations() {
            gsap.fromTo(".contact-title",
                { y: 50, opacity: 0 },
                {
                    y: 0,
                    opacity: 1,
                    duration: 1,
                    ease: "power3.out",
                    scrollTrigger: {
                        trigger: "#contact",
                        start: "top 80%",
                    }
                }
            );

            gsap.fromTo(".contact-line",
                { scaleX: 0 },
                {
                    scaleX: 1,
                    duration: 1,
                    delay: 0.2,
                    ease: "power3.out",
                    scrollTrigger: {
                        trigger: "#contact",
                        start: "top 80%",
                    }
                }
            );

            gsap.fromTo(".contact-info > *",
                { y: 50, opacity: 0 },
                {
                    y: 0,
                    opacity: 1,
                    duration: 0.8,
                    stagger: 0.15,
                    ease: "power3.out",
                    scrollTrigger: {
                        trigger: ".contact-info",
                        start: "top 85%",
                    }
                }
            );

            gsap.fromTo(".contact-form",
                { y: 80, opacity: 0, rotateX: 15 },
                {
                    y: 0,
                    opacity: 1,
                    rotateX: 0,
                    duration: 1.2,
                    ease: "expo.out",
                    transformPerspective: 1000,
                    scrollTrigger: {
                        trigger: ".contact-form",
                        start: "top 85%",
                    }
                }
            );
        }
    }
}
</script>

<style scoped>
.contact-section {
    position: relative;
    background-color: transparent;
    color: var(--text-primary);
    font-family: sans-serif;
    min-height: 100vh;
    padding: 8rem 5vw;
}

@media (min-width: 768px) {
    .contact-section {
        padding: 8rem 10vw;
    }
}

.contact-container {
    width: 100%;
    max-width: 56rem;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    position: relative;
    z-index: 10;
    text-align: center;
}

.title-container-contact {
    margin-bottom: 3rem;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.contact-title {
    color: var(--text-primary);
    font-size: 2.25rem;
    font-weight: 700;
    line-height: 1.25;
    letter-spacing: -0.025em;
    margin: 0;
}

@media (min-width: 768px) {
    .contact-title {
        font-size: 3rem;
    }
}

@media (min-width: 1024px) {
    .contact-title {
        font-size: 3.75rem;
    }
}

.contact-line {
    height: 0.25rem;
    width: 6rem;
    background-color: var(--accent-hover);
    margin-top: 1.5rem;
    border-radius: 9999px;
}

.contact-info {
    width: 100%;
    margin-bottom: 4rem;
    display: flex;
    flex-direction: column;
    gap: 3rem;
}

.contact-header {
    max-width: 42rem;
    margin: 0 auto;
}

.contact-subtitle {
    font-size: 1.875rem;
    font-weight: 700;
    color: var(--text-primary);
    margin-bottom: 1rem;
}

.contact-desc {
    color: var(--text-muted);
    font-size: 1.125rem;
    line-height: 1.625;
    margin: 0;
}

.contact-cards {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1.5rem;
    padding: 0 1rem;
}

@media (min-width: 640px) {
    .contact-cards {
        flex-direction: row;
    }
}

.contact-card {
    width: 100%;
    max-width: 320px;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    gap: 1rem;
    padding: 2rem;
    border-radius: 1.5rem;
    background-color: var(--card-bg-solid);
    backdrop-filter: blur(12px);
    border: 1px solid var(--bg-card);
    color: var(--text-secondary);
    transition: all 0.3s ease;
    box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
    text-decoration: none;
}

@media (min-width: 640px) {
    .contact-card {
        flex: 1 1 0%;
    }
}

.contact-card:hover {
    color: var(--accent);
    border-color: var(--hover-bg);
    background-color: var(--card-bg-solid);
}

.contact-icon-wrapper {
    width: 4rem;
    height: 4rem;
    border-radius: 1rem;
    background-color: var(--icon-bg);
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s ease;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

.contact-card:hover .contact-icon-wrapper {
    background-color: var(--hover-bg);
    transform: scale(1.1);
}

.contact-icon {
    width: 1.75rem;
    height: 1.75rem;
}

.contact-card-text {
    display: flex;
    flex-direction: column;
}

.contact-card-label {
    font-size: 0.875rem;
    color: #64748b;
    font-weight: 500;
    margin-bottom: 0.25rem;
    margin-top: 0;
}

.contact-card-value {
    font-size: 1rem;
    font-weight: 600;
    letter-spacing: 0.025em;
}

@media (min-width: 768px) {
    .contact-card-value {
        font-size: 0.875rem;
    }
}

@media (min-width: 1024px) {
    .contact-card-value {
        font-size: 1rem;
    }
}

.contact-form-wrapper {
    width: 100%;
    max-width: 48rem;
}

.contact-form {
    text-align: left;
    background-color: var(--bg-nav);
    backdrop-filter: blur(24px);
    padding: 2rem;
    border-radius: 1.5rem;
    border: 1px solid var(--border-color);
    box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
    position: relative;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
}

@media (min-width: 768px) {
    .contact-form {
        padding: 2.5rem;
    }
}

.form-glow {
    position: absolute;
    inset: 0;
    background: linear-gradient(to bottom right, var(--hover-bg), transparent);
    opacity: 0;
    transition: opacity 0.7s ease;
    pointer-events: none;
}

.contact-form:hover .form-glow {
    opacity: 1;
}

.form-row {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1.5rem;
}

@media (min-width: 768px) {
    .form-row {
        grid-template-columns: repeat(2, 1fr);
    }
}

.form-group {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    position: relative;
    z-index: 1;
}

.form-group label {
    font-size: 0.875rem;
    font-weight: 600;
    color: var(--text-secondary);
    margin-left: 0.25rem;
}

.form-input {
    width: 100%;
    background-color: var(--bg-glass);
    border: 1px solid var(--bg-card);
    border-radius: 1rem;
    padding: 1rem 1.25rem;
    color: var(--text-primary);
    transition: all 0.3s ease;
    outline: none;
    font-family: inherit;
    font-size: 1rem;
    box-sizing: border-box;
}

.form-input::placeholder {
    color: #475569;
}

.form-input:focus {
    border-color: var(--border-hover);
    box-shadow: 0 0 0 1px var(--border-hover);
}

.form-textarea {
    resize: none;
}

.form-submit {
    width: 100%;
    background-color: var(--accent-hover);
    color: var(--bg-primary);
    font-weight: 700;
    font-size: 1.125rem;
    padding: 1rem 0;
    border-radius: 1rem;
    transition: all 0.3s ease;
    box-shadow: 0 0 20px var(--border-hover);
    margin-top: 0.5rem;
    cursor: pointer;
    border: none;
    position: relative;
    z-index: 1;
}

.form-submit:hover {
    background-color: var(--accent);
    transform: scale(1.02);
    box-shadow: 0 0 30px var(--border-hover);
}

.form-submit:active {
    transform: scale(0.98);
}
</style>
