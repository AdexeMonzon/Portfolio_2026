# Justificación de Decisiones de Diseño y Desarrollo
## Portfolio Personal 2026 - Adexe Monzón Santana

Este documento detalla las decisiones técnicas y de diseño tomadas durante el desarrollo del portfolio, justificando la aplicación de los principios fundamentales de diseño de interfaces web, usabilidad y accesibilidad.

---

### 1. Planificación del Diseño
La creación del portfolio se ha basado en una planificación meticulosa orientada a transmitir una imagen profesional, moderna y tecnológicamente avanzada.

*   **Metodología de Desarrollo:** Se ha optado por un enfoque **basado en componentes** utilizando **Vue 3** y **Vite**. Esta decisión permite una estructura modular donde cada sección (Home, About, Skills, Experience, Projects) es independiente y reutilizable, facilitando el mantenimiento y la escalabilidad del proyecto.
*   **Enfoque Mobile-First:** El diseño se planificó inicialmente para dispositivos móviles, expandiéndose progresivamente hacia pantallas de escritorio. Se han utilizado técnicas de **Flexbox** y **CSS Grid** para asegurar que el layout sea fluido y se adapte a cualquier resolución, garantizando que el contenido principal siempre esté centrado y sea el foco de atención.
*   **Organización del Contenido:** El flujo de navegación se ha diseñado de forma lineal (Single Page Application) para facilitar la lectura y el "storytelling" de la trayectoria profesional del autor.

### 2. Coherencia Visual
Para lograr una interfaz profesional y armoniosa, se ha definido un sistema de diseño consistente.

*   **Identidad Visual:** Se ha seleccionado una paleta de colores basada en contrastes profundos. En el modo oscuro, predominan los tonos *slate* y *emerald* para los acentos, mientras que en el modo claro se utilizan tonos neutros y azules eléctricos.
*   **Tokens de Diseño:** Se ha implementado un sistema de **Variables CSS (Custom Properties)** centralizado en `style.css`. Esto garantiza que elementos como el radio de los bordes, los colores de fondo y las sombras sean idénticos en todos los componentes.
*   **Efectos Premium:** Se ha integrado la estética **Glassmorphism** (efecto cristal esmerilado) en componentes como la barra de navegación y las tarjetas de proyectos (`GlassSurface.vue`), aportando profundidad y una sensación de modernidad sin saturar la interfaz.

### 3. Aplicación de Estilos
El desarrollo de estilos ha evolucionado de un uso inicial de utilidades hacia un sistema de **CSS puro y mantenible**.

*   **Tematización Dinámica:** Se ha desarrollado un motor de temas (oscuro/claro) que no solo cambia los colores, sino que ajusta las opacidades y los efectos visuales para mantener la legibilidad. La transición entre temas es fluida gracias a animaciones CSS de `0.5s`.
*   **Tipografía:** Se han seleccionado fuentes modernas del catálogo de Google Fonts, aplicadas mediante unidades relativas (`rem`), asegurando que el ritmo vertical y la jerarquía visual se mantengan estables en cualquier dispositivo.
*   **Micro-animaciones:** Se han utilizado herramientas como **GSAP (GreenSock Animation Platform)** para crear transiciones suaves al hacer scroll, lo que mejora la percepción de calidad del sitio y guía la vista del usuario hacia los elementos importantes.

### 4. Tratamiento e Integración de Contenido Multimedia
El contenido multimedia es el eje central de la experiencia visual del portfolio.

*   **Gráficos 3D y WebGL:** Se ha integrado un fondo dinámico (`LightPilar.vue`) utilizando **Three.js**. Este elemento multimedia no es solo estético; reacciona a los cambios de tema y aporta una capa de interactividad técnica que demuestra las capacidades de desarrollo del autor.
*   **Optimización de Imágenes:**
    *   Uso preferente de **SVG** para iconos de tecnologías y navegación, garantizando nitidez total y peso mínimo.
    *   Tratamiento de imágenes de perfil y proyectos mediante máscaras CSS y filtros dinámicos, evitando la carga de archivos con transparencias pesadas.
*   **Interactividad Multimedia:** Los proyectos se presentan a través de un **carrusel interactivo (Swiper)** integrado en modales, permitiendo una exploración detallada de las capturas de pantalla sin interrumpir el flujo de navegación principal.

### 5. Accesibilidad y Usabilidad
El sitio ha sido diseñado para ser inclusivo y fácil de usar por cualquier persona.

*   **Accesibilidad (A11y):**
    *   **Semántica HTML5:** Uso de etiquetas estructurales (`<main>`, `<section>`, `<nav>`, `<footer>`) para una correcta interpretación por parte de motores de búsqueda y lectores de pantalla.
    *   **Atributos ARIA:** Se han incluido etiquetas `aria-label` en elementos puramente visuales o interactivos (como el selector de idioma o el toggle de tema) para mejorar la experiencia de usuarios con diversidad funcional.
    *   **Contraste Lumínico:** Se ha verificado que la relación de contraste entre texto y fondo cumpla con los estándares WCAG, incluso en el modo claro.
*   **Usabilidad (UX):**
    *   **Feedback Inmediato:** El usuario recibe confirmación visual de cada acción (efectos de *hover*, animaciones de carga, transiciones de página).
    *   **Navegación Intuitiva:** La barra de navegación es persistente pero discreta, permitiendo el acceso rápido a cualquier sección. En dispositivos móviles, se transforma en un menú hamburguesa optimizado para el uso con el pulgar.
    *   **Rendimiento:** Se ha minimizado el uso de librerías pesadas y se ha optimizado el renderizado de los componentes 3D para asegurar una experiencia fluida incluso en dispositivos de gama media.
