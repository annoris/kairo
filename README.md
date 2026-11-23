<div align="center">
  <img src="./kairo/logo.svg" alt="KAIRO Logo" width="200" />
  <h1>KAIRO — Spatial Web &amp; 3D Interactive Experience</h1>
  <p>
    <strong>Creative Technologist &amp; Spatial Web Engineer — Sculpting kinetic interfaces and spatial web experiences.</strong>
  </p>

  <p>
    <img src="https://img.shields.io/badge/Next.js-14-0B0C10?style=for-the-badge&logo=nextdotjs&logoColor=F2EFE9" alt="Next.js 14" />
    <img src="https://img.shields.io/badge/Three.js-r167-0B0C10?style=for-the-badge&logo=threedotjs&logoColor=E5C17B" alt="Three.js" />
    <img src="https://img.shields.io/badge/WebGL%20%2F%20GLSL-Shaders-FF5722?style=for-the-badge&logo=webgl&logoColor=0B0C10" alt="WebGL / GLSL" />
    <img src="https://img.shields.io/badge/GSAP-3.12-0B0C10?style=for-the-badge&logo=greensock&logoColor=E5C17B" alt="GSAP" />
    <img src="https://img.shields.io/badge/Lenis-Smooth%20Scroll-161822?style=for-the-badge&logoColor=F2EFE9" alt="Lenis" />
    <img src="https://img.shields.io/badge/UI-Dark%20Luxury-0B0C10?style=for-the-badge&color=E5C17B" alt="Dark Luxury UI" />
  </p>

  <p>
    <a href="#-galería-visual--carpeta-kairo">Galería Visual</a> ·
    <a href="#-cómo-funciona-la-arquitectura">Arquitectura Técnica</a> ·
    <a href="./ARCHITECTURE.md">Deep-Dive Técnico</a> ·
    <a href="#-acceso-al-repositorio-privado-descarga-del-código-fuente">Acceso al Código Privado</a>
  </p>
</div>

---

![KAIRO Live Showcase](./kairo/kairo-preview.gif)

---

## ✨ ¿Qué es KAIRO?

**KAIRO** (`kairo.studio`) es una experiencia web espacial de nivel **Awwwards** diseñada con estética **Dark Luxury** (`#0B0C10` obsidiana, `#F2EFE9` alabastro, `#E5C17B` oro cepillado y `#FF5722` bermellón cinético).

Combina renderizado **WebGL / Three.js en tiempo real**, simulación física de fluidos **Navier-Stokes** reactiva al cursor, shaders **GLSL Perlin**, física 3D con **Rapier**, coreografía de scroll con **GSAP + Lenis** y un sistema de tokens CSS dinámicos que transforma toda la atmósfera cromática de la web en cada caso de estudio.

> 📌 **Nota importante:** Este repositorio público ([`annoris/kairo`](https://github.com/annoris/kairo)) contiene la **documentación arquitectónica completa**, el **GIF showcase** y la **carpeta pública [`kairo/`](./kairo/)** con todos los visuales HD. El código fuente completo descargable vive en el **repositorio privado [`annoris/kairo-pro`](https://github.com/annoris/kairo-pro)** (acceso exclusivo para contribuidores; consulta la sección de [Acceso al Repositorio Privado](#-acceso-al-repositorio-privado-descarga-del-código-fuente)).

---

## 🎨 Galería Visual — Carpeta `kairo/`

Todos los visuales de alta definición están abiertos y disponibles dentro de [`./kairo/`](./kairo/) para que puedas explorar la dirección de arte y el sistema visual completo de la experiencia:

### Identidad &amp; Estudio

| Retrato Editorial (`kairo/portrait.webp`) | Estudio Panorámico (`kairo/hero-studio.webp`) |
| :---: | :---: |
| <img src="./kairo/portrait.webp" alt="Kairo Vance Portrait" width="380" /> | <img src="./kairo/hero-studio.webp" alt="KAIRO Zurich Studio" width="380" /> |

### Casos de Estudio (5 Proyectos Interactivos)

| Proyecto | Disciplina &amp; Paleta | Preview HD |
| :--- | :--- | :---: |
| **AURA ATELIER** | Spatial 3D Flagship &amp; WebGL Interior Showroom<br/>`#0B0C10` · `#E5C17B` · `#FF5722` | <img src="./kairo/aura-atelier.webp" alt="Aura Atelier" width="340" /> |
| **SYNTHOS OS** | Spatial AI Analytics &amp; Real-Time Control Engine<br/>`#0E1017` · `#C4B5FD` · `#6366F1` | <img src="./kairo/synthos-os.webp" alt="Synthos OS" width="340" /> |
| **MONOLITH CAD** | Interactive 3D Architectural Modeling Platform<br/>`#110E14` · `#FDE68A` · `#D97706` | <img src="./kairo/monolith-cad.webp" alt="Monolith CAD" width="340" /> |
| **VELOURA LABS** | Biotech Luxury Skincare Interactive Commerce<br/>`#0A1112` · `#67E8F9` · `#06B6D4` | <img src="./kairo/veloura-labs.webp" alt="Veloura Labs" width="340" /> |
| **PULSAR ENGINE** | Real-Time Market Telemetry &amp; Data Visualization<br/>`#120E0D` · `#FDA4AF` · `#E11D48` | <img src="./kairo/pulsar-engine.webp" alt="Pulsar Engine" width="340" /> |

---

## 🧠 Cómo Funciona la Arquitectura

KAIRO ejecuta dos capas sincronizadas a **60fps** — una capa **DOM editorial** y un **Canvas WebGL persistente** — orquestadas por **Zustand**, **Lenis** y **GSAP ScrollTrigger**:

```mermaid
flowchart TB
    User["Interacción del Usuario\n(Cursor, Scroll, Navegación)"] --> Lenis["Lenis Smooth Scroll\n(Inercia + Tempus RAF)"]
    User --> FluidInput["Pointer Velocity Tracker\n(Inyección de Impulsos)"]

    subgraph Core["Núcleo React + Next.js 14"]
        Store["Zustand Global Store\n(isLoading, introOut, isMenuOpen, fluidColor)"]
        DOM["Capa DOM Editorial\nGSAP ScrollTrigger · SplitType · Tokens Dark Luxury"]
        Canvas["Capa WebGL (React Three Fiber)\nCanvas Fijo Full-Viewport"]
    end

    Lenis --> DOM
    Store <--> DOM
    Store <--> Canvas

    subgraph GPU["Pipeline GPU & Física"]
        Perlin["GLSL Perlin Noise Shader\n(Atmósfera de Fondo)"]
        Navier["Navier-Stokes Fluid FBOs\n(Advección · Divergencia · Presión · Gradiente)"]
        Rapier["Rapier 3D Physics (WASM)\n(Cuerpos Rígidos Interactivos)"]
    end

    FluidInput --> Navier
    Canvas --> Perlin
    Canvas --> Navier
    Canvas --> Rapier
```

### Pilares Técnicos

1. **Shaders GLSL &amp; Fondo Perlin**: Plano WebGL a pantalla completa impulsado por ruido Perlin procedural en fragment shaders personalizados, aportando profundidad orgánica sin cargar videos pesados.
2. **Simulación de Fluidos Navier-Stokes**: Pipeline multi-pasada en GPU con Frame Buffer Objects (FBOs) *ping-pong* (advección de velocidad, divergencia, iteración de presión Jacobi, resta de gradiente y *splats* del cursor) integrado como efecto de postprocesado en `@react-three/postprocessing`.
3. **Física 3D con Rapier (`@react-three/rapier`)**: Motor de física WebAssembly que simula gravedad, colisiones e impulsos en tiempo real sin bloquear el hilo principal de JavaScript.
4. **Animaciones GSAP + ScrollTrigger + SplitType**: Revelado cinético línea por línea (`AppearTitle`), transición de pantalla completa en el `Loader` (`0% → 100%`), menú lateral con escala 3D (`scale: 0.9` y borde `#FF5722`) y tarjetas de proyectos apiladas sincronizadas al scroll.
5. **Lenis Smooth Scroll**: Inercia mantecosa unificada con `ScrollTrigger` sobre un contenedor `main` dedicado y bucle `requestAnimationFrame` centralizado con `@darkroom.engineering/tempus`.
6. **Sistema de Tokens Dark Luxury Dinámico**: Variables CSS globales (`--white`, `--black`, `--accentColor`, `--fillColor`, `--menuColor`, `--menuFontColor`) que mutan en vivo al abrir cada proyecto junto con el color del fluido WebGL (`setFluidColor`).

> 📖 Lee el desglose técnico completo en **[`ARCHITECTURE.md`](./ARCHITECTURE.md)**.

---

## 🔒 Acceso al Repositorio Privado (Descarga del Código Fuente)

Este repositorio público (**[`annoris/kairo`](https://github.com/annoris/kairo)**) existe para compartir **la arquitectura completa, el GIF showcase, los estándares de diseño y la carpeta visual [`kairo/`](./kairo/)** con toda la comunidad.

El **código fuente completo y descargable** (componentes Next.js 14, shaders GLSL, simulación Navier-Stokes, escenas R3F/Rapier y configuración lista para producción) se mantiene en el **repositorio privado exclusivo [`annoris/kairo-pro`](https://github.com/annoris/kairo-pro)**.

### ¿Cómo desbloquear la invitación a `annoris/kairo-pro`?

**Solo quienes contribuyan activamente al proyecto reciben acceso al repositorio privado [`annoris/kairo-pro`](https://github.com/annoris/kairo-pro).** Puedes calificar mediante cualquiera de estas contribuciones:

- 🛠️ **Pull Request de valor** en [`annoris/kairo`](https://github.com/annoris/kairo) (mejoras a la documentación técnica, diagramas, guías de shaders, traducciones o casos de estudio).
- 🎨 **Aportes de diseño / feedback técnico profundo** abriendo un Issue detallado en [`annoris/kairo`](https://github.com/annoris/kairo/issues) con propuestas de UX, optimización WebGL o accesibilidad.
- 🤝 **Colaboración técnica o patrocinio** para impulsar el desarrollo de la plataforma.

👉 Revisa las instrucciones paso a paso en **[`CONTRIBUTING.md`](./CONTRIBUTING.md)** para enviar tu contribución y recibir tu invitación a **`annoris/kairo-pro`**.

---

<div align="center">
  <p>Si este showcase y su arquitectura te inspiraron, dale una ⭐ al repositorio.</p>
  <sub>KAIRO · Zurich, Switzerland · <a href="mailto:hello@kairo.studio">hello@kairo.studio</a></sub>
</div>
