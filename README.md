# Portfolio Personal - Adexe Monzón Santana

Este proyecto es mi portfolio personal desarrollado con **Vue 3**, **Vite** y **CSS**. Ha sido diseñado y programado desde cero aplicando los principios del desarrollo frontend moderno, centrándose en el rendimiento, la estética y la experiencia de usuario.

A continuación, se detalla la justificación técnica del proyecto orientada a la consecución de los **Resultados de Aprendizaje (RA)** del módulo de Diseño de Interfaces Web:

---

## Justificación de Resultados de Aprendizaje

### RA1: Planifica la creación de una interfaz web valorando y aplicando especificaciones de diseño.
La arquitectura del proyecto se planificó bajo un enfoque **basado en componentes** (Vue.js), permitiendo una estructura modular y escalable. 
- Se diseñó previamente la paleta de colores, la tipografía (fuentes modernas *sans-serif*) y la jerarquía visual.
- Se ha aplicado un diseño **Mobile-First**, utilizando `Flexbox` y `CSS Grid` para planificar el comportamiento responsivo del layout desde pantallas de móviles hasta monitores Ultrawide, garantizando que cada sección (Inicio, Tecnologías, Proyectos) ocupe el 100% de la pantalla (`100vh`) de forma centrada y estructurada.

### RA2: Crea interfaces Web homogéneos definiendo y aplicando estilos.
Para asegurar la homogeneidad visual en todo el sitio, se ha implementado un sistema de diseño robusto mediante **variables CSS (Custom Properties)**.
- Se han centralizado los tokens de diseño (`--bg-primary`, `--text-primary`, `--accent`, etc.) permitiendo que componentes independientes compartan exactamente los mismos estilos.
- Se implementó un **tema claro/oscuro dinámico** que reasigna estas variables en tiempo real, manteniendo la legibilidad y la identidad visual (como el estilo *Glassmorphism* y el color de acento) coherentes a lo largo de toda la aplicación, sin estilos "huérfanos".

### RA3: Prepara archivos multimedia para la Web, analizando sus características y manejando herramientas específicas.
Los recursos multimedia del portfolio han sido seleccionados y preparados teniendo en cuenta el rendimiento y la calidad.
- Se ha priorizado el formato **SVG** para toda la iconografía (iconos de tecnologías, botones de la navbar, GitHub, flechas de experiencia) asegurando un peso mínimo y un escalado infinito sin pérdida de calidad.
- Las imágenes fotográficas y capturas de proyectos han sido ajustadas en relación de aspecto e integradas mediante técnicas CSS avanzadas (por ejemplo, aplicación de máscaras `mask-image` y `drop-shadow` dinámicos en la foto de perfil) para una integración perfecta sin requerir pesados archivos PNG con transparencias renderizadas externamente.

### RA4: Integra contenido multimedia en documentos Web valorando su aportación y seleccionando adecuadamente los elementos interactivos.
El contenido multimedia no es estático, sino que aporta valor interactivo:
- Se ha integrado un componente 3D dinámico (`LightPilar.vue`) basado en WebGL (Three.js/GLSL) que reacciona a los colores del tema de la web, aportando profundidad y una estética premium al fondo sin interferir en la lectura.
- Los proyectos del portfolio utilizan un **carrusel de imágenes personalizado** (Swiper) dentro de una ventana modal, permitiendo al usuario interactuar y explorar diferentes capturas de pantalla de un mismo proyecto sin abandonar la página actual.
- Se han integrado animaciones fluidas con la biblioteca **GSAP (ScrollTrigger)**, haciendo que el contenido multimedia aparezca progresivamente a medida que el usuario interactúa con la página.

### RA5: Desarrolla interfaces Web accesibles, analizando las pautas establecidas y aplicando técnicas de verificación.
El portfolio ha sido desarrollado teniendo en cuenta estándares de accesibilidad:
- **Estructura semántica:** Uso correcto de etiquetas HTML5 (`<main>`, `<section>`, `<nav>`, `<h1>` para el título principal y jerarquía correcta de encabezados).
- **Soporte para lectores de pantalla:** Se han añadido atributos `aria-label` en elementos de interacción visual como el botón del menú hamburguesa y el botón para cambiar de tema.
- **Contraste adaptativo:** El diseño garantiza un alto contraste tanto en modo oscuro como en modo claro, calculando incluso la opacidad dinámica del componente 3D para evitar que deslumbre o dificulte la lectura del texto superpuesto.
- **Unidades relativas:** Las tipografías están construidas mediante unidades `rem` para adaptarse a las configuraciones de tamaño de texto del navegador del usuario.

### RA6: Desarrolla interfaces Web amigables analizando y aplicando las pautas de usabilidad establecidas.
La usabilidad ha sido un pilar fundamental durante el desarrollo:
- **Navegación clara:** Se implementó una barra de navegación fija y transparente (*Glassmorphism*) que permite al usuario saber siempre dónde está. En dispositivos móviles, se transforma de manera amigable en un menú desplegable (botón hamburguesa).
- **Feedback visual constante:** Todas las interacciones del usuario reciben una respuesta inmediata (cambios de color en *hover*, cursores pointer, animaciones de pulsación, y flechas indicadoras que rotan al desplegar descripciones en la sección de experiencia).
- **Prevención de errores de interfaz:** Se han bloqueado posibles problemas de usabilidad clásicos, como la aparición de *scrolls laterales* involuntarios en móviles, aplicando técnicas de control de *overflow* y anchos máximos.

---
## Instalación y Despliegue

```sh
# Instalar dependencias
npm install

# Compilar y arrancar el servidor en desarrollo
npm run dev
```
