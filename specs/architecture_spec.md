# 🏗️ Especificación Técnica de Arquitectura — Suena v2
## Reconstrucción desde Cero · Septiembre 2026

> **Documento de referencia para el Frontend Developer.**
> Todo lo aquí definido es implementable literalmente — copiar CSS, seguir estructura HTML, implementar JS.

---

## 📋 Resumen Ejecutivo

| Aspecto | Decisión |
|---------|----------|
| **Tipo** | HTML self-contained (~300-400 KB sin imágenes, ~15 MB con imágenes base64) |
| **Framework** | Ninguno — JS vanilla + CSS custom properties |
| **Content strategy** | 28 Markdowns pre-convertidos a HTML con Python (NO marked.js) |
| **Progressive disclosure** | Acordeones automáticos en H3, tabs en grupos, secciones "🚀" colapsadas |
| **Interactividad** | Scroll-reveals, micro-interacciones, gamificación, easter eggs, confetti |
| **Responsive** | Mobile-first, 4 breakpoints: 480px, 768px, 1024px, 1280px |
| **Tokens** | 100% de los 80 CSS custom properties del brand guide usados con var() |
| **Dark mode** | [data-theme="dark"] con 28 overrides |
| **Accesibilidad** | WCAG AA: ARIA, keyboard nav, focus management, 44px touch targets |

---

## 1. 🏛️ Arquitectura HTML

### 1.1 Estructura del DOM

```html
<!DOCTYPE html>
<html lang="es" data-theme="light">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Suena — Tu Espacio Musical</title>
  <!-- Google Fonts (único CDN permitido) -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400&family=Nunito:wght@700;800&display=swap" rel="stylesheet">
  <style>/* === ALL CSS INLINE === */</style>
</head>
<body>
  <!-- Skip to content (accessibility) -->
  <a href="#main-content" class="skip-link">Saltar al contenido</a>

  <!-- Overlay for mobile sidebar -->
  <div class="overlay" id="overlay" aria-hidden="true"></div>

  <!-- SIDEBAR NAVIGATION -->
  <nav class="sidebar" id="sidebar" role="navigation" aria-label="Menú de navegación">
    <div class="sidebar-header">
      <h1 class="sidebar-brand">🎵 Suena</h1>
      <p class="sidebar-tagline">Tu Espacio Musical</p>
      <!-- Progress indicator -->
      <div class="sidebar-progress">
        <div class="progress-bar"><div class="progress-fill" id="progressFill"></div></div>
        <span class="progress-text" id="progressText">0 de 28</span>
      </div>
    </div>

    <!-- Nav groups (collapsible) -->
    <div class="nav-groups" id="navGroups">
      <!-- Each group: -->
      <div class="nav-group" data-group="fundamentos">
        <button class="nav-group-toggle" aria-expanded="false">
          <span class="nav-group-icon">🎵</span>
          <span class="nav-group-label">Fundamentos</span>
          <span class="nav-group-chevron">▸</span>
          <span class="nav-group-badge" data-visited="0/4">0/4</span>
        </button>
        <div class="nav-group-items" role="list">
          <a class="nav-item" data-section="fundamentos-pulso" role="listitem">El Pulso</a>
          <a class="nav-item" data-section="fundamentos-ritmo" role="listitem">Ritmo</a>
          <a class="nav-item" data-section="fundamentos-melodia" role="listitem">Melodía</a>
          <a class="nav-item" data-section="fundamentos-lectura" role="listitem">Lectura Musical</a>
        </div>
      </div>
      <!-- Repeat for each group -->
    </div>

    <!-- Theme toggle -->
    <div class="sidebar-footer">
      <button class="theme-toggle" id="themeToggle" aria-label="Cambiar tema">
        <span class="theme-icon">🌙</span>
        <span class="theme-label">Modo Oscuro</span>
      </button>
    </div>
  </nav>

  <!-- MAIN CONTENT -->
  <main class="main" id="main-content" role="main">
    <!-- Top bar (mobile) -->
    <header class="topbar" role="banner">
      <button class="hamburger" id="hamburger" aria-label="Abrir menú" aria-expanded="false">
        <span class="hamburger-line"></span>
        <span class="hamburger-line"></span>
        <span class="hamburger-line"></span>
      </button>
      <div class="search-wrapper" role="search">
        <input type="search" class="search-input" id="searchInput" 
               placeholder="🔍 Buscar..." aria-label="Buscar en el sitio">
        <div class="search-results" id="searchResults" role="listbox" aria-label="Resultados"></div>
      </div>
    </header>

    <!-- Content sections -->
    <article class="section" data-section="inicio" id="section-inicio">
      <div class="section-content container">
        <!-- Hero (only on inicio) -->
        <div class="hero">...</div>
        <!-- Pre-rendered HTML content -->
      </div>
      <!-- Navigation footer -->
      <nav class="section-nav" aria-label="Navegación de sección">
        <a class="section-nav-next" data-next="fundamentos-pulso">
          Siguiente: 🎵 El Pulso →
        </a>
      </nav>
    </article>

    <article class="section" data-section="fundamentos-pulso" id="section-fundamentos-pulso" hidden>
      <div class="section-content container">
        <!-- Breadcrumb -->
        <nav class="breadcrumb" aria-label="Ubicación">
          <a data-nav="inicio">🏠</a> › <a data-nav="fundamentos">Fundamentos</a> › <span>El Pulso</span>
        </nav>
        <!-- Section image -->
        <img class="section-hero-img" src="data:image/png;base64,..." 
             alt="Ilustración de ondas sonoras y ritmo" loading="lazy">
        <!-- Pre-rendered HTML content (with auto-accordions on H3) -->
      </div>
      <!-- Section navigation -->
      <nav class="section-nav" aria-label="Navegación de sección">
        <a class="section-nav-prev" data-prev="inicio">← Inicio</a>
        <span class="section-counter">2 de 28</span>
        <a class="section-nav-next" data-next="fundamentos-ritmo">Siguiente: Ritmo →</a>
      </nav>
    </article>

    <!-- ... 26 more sections ... -->
  </main>

  <!-- Back to top -->
  <button class="back-to-top" id="backToTop" aria-label="Volver arriba">↑</button>

  <!-- Footer -->
  <footer class="footer" role="contentinfo">
    <p class="footer-quote" id="footerQuote"></p>
    <p class="footer-meta">Suena — Tu Espacio Musical · Taller de Música · Bachillerato UADY</p>
  </footer>

  <!-- Confetti canvas (hidden, used by JS) -->
  <canvas class="confetti-canvas" id="confettiCanvas" aria-hidden="true"></canvas>

  <script>/* === ALL JS AT THE END === */</script>
</body>
</html>
```

### 1.2 Naming Convention

| Element | Pattern | Example |
|---------|---------|---------|
| Section IDs | `section-{group}-{name}` | `section-fundamentos-pulso` |
| Data attributes | `data-section="{id}"` | `data-section="fundamentos-pulso"` |
| Nav groups | `data-group="{group}"` | `data-group="fundamentos"` |
| CSS classes | BEM-lite: `block-element--modifier` | `nav-item--active` |
| JS IDs | camelCase | `searchInput`, `progressFill` |

### 1.3 Section Order (28 sections)

```
 #  | ID                           | Group          | Prev/Next
----|------------------------------|----------------|----------
 1  | inicio                       | —              | —/fundamentos-pulso
 2  | fundamentos-pulso            | fundamentos    | inicio/fundamentos-ritmo
 3  | fundamentos-ritmo            | fundamentos    | .../fundamentos-melodia
 4  | fundamentos-melodia          | fundamentos    | .../fundamentos-lectura
 5  | fundamentos-lectura          | fundamentos    | .../voz-tecnica
 6  | voz-tecnica                  | voz            | .../voz-adolescente
 7  | voz-adolescente              | voz            | .../voz-coro
 8  | voz-coro                     | voz            | .../instrumento-guitarra
 9  | instrumento-guitarra         | instrumentos   | .../instrumento-piano
10  | instrumento-piano            | instrumentos   | .../instrumento-bajo
11  | instrumento-bajo             | instrumentos   | .../instrumento-percusion
12  | instrumento-percusion        | instrumentos   | .../ensamble
13  | ensamble                     | ensamble       | .../armonia-acordes
14  | armonia-acordes              | armonia        | .../armonia-progresiones
15  | armonia-progresiones         | armonia        | .../armonia-arreglos
16  | armonia-arreglos             | armonia        | .../creatividad-improvisacion
17  | creatividad-improvisacion    | creatividad    | .../creatividad-composicion
18  | creatividad-composicion      | creatividad    | .../creatividad-fusion
19  | creatividad-fusion           | creatividad    | .../formato-perfil
20  | formato-perfil               | formatos       | .../formato-autoeval1
21  | formato-autoeval1            | formatos       | .../formato-autoeval2
22  | formato-autoeval2            | formatos       | .../formato-coeval-ensayo
23  | formato-coeval-ensayo        | formatos       | .../formato-coeval-presentacion
24  | formato-coeval-presentacion  | formatos       | .../formato-bitacora
25  | formato-bitacora             | formatos       | .../recursos-herramientas
26  | recursos-herramientas        | recursos       | .../recursos-presentaciones
27  | recursos-presentaciones      | recursos       | .../glosario
28  | glosario                     | glosario       | .../—
```

### 1.4 Progressive Disclosure Rules

| Rule | Behavior |
|------|----------|
| **Sections** | Only 1 visible at a time (display: block/none with `hidden` attribute) |
| **H3 auto-accordion** | Every `<h3>` within a section becomes an accordion header. Content between H3s collapses. First H3 open by default, rest closed. |
| **"🚀 Para los que quieren más"** | Auto-detected by content pattern. Always starts collapsed. Badge: "Avanzado" |
| **Tables > 4 rows** | Auto-collapsed with "Ver tabla completa" toggle |
| **Sidebar nav groups** | Collapsed by default. Only the active group is auto-expanded. |
| **Long sections (>2000 words)** | Show TL;DR summary (first paragraph) + "Leer más" button |

---

## 2. 🎨 CSS Architecture

### 2.1 Complete CSS — Design System Foundation

```css
/* ============================================================
   SUENA v2 — DESIGN SYSTEM CSS
   All values use brand tokens. ZERO hardcoded values.
   ============================================================ */

/* === TOKENS === */
:root {
  /* Colors */
  --color-primary: #E8614D;
  --color-primary-dark: #C94A36;
  --color-primary-light: #FCEAE7;
  --color-secondary: #2D3A4A;
  --color-secondary-light: #4A6078;
  --color-accent: #2EC4A0;
  --color-accent-dark: #22957A;
  --color-accent-light: #E6F9F4;
  --color-bg: #FAFAF8;
  --color-surface: #F2F2EF;
  --color-surface-elevated: #FFFFFF;
  --color-border: #E0DDD8;
  --color-border-light: #EDECEA;
  --color-text-primary: #1A1A1A;
  --color-text-secondary: #5C5C5C;
  --color-text-tertiary: #8C8C8C;
  --color-text-inverse: #FFFFFF;
  --color-success: #2EC4A0;
  --color-success-light: #E6F9F4;
  --color-warning: #F5A623;
  --color-warning-light: #FEF5E4;
  --color-error: #E04848;
  --color-error-light: #FDECEC;
  --color-nivel-c-bg: #E6F9F4;
  --color-nivel-c-text: #22957A;
  --color-nivel-b-bg: #FEF5E4;
  --color-nivel-b-text: #B8820C;
  --color-nivel-a-bg: #EDE8FD;
  --color-nivel-a-text: #6B4FBB;

  /* Gradients */
  --gradient-hero: linear-gradient(135deg, #E8614D 0%, #2D3A4A 100%);
  --gradient-section: linear-gradient(135deg, #FCEAE7 0%, #E6F9F4 100%);

  /* Typography */
  --font-heading: 'Nunito', system-ui, sans-serif;
  --font-body: 'Inter', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', 'Courier New', monospace;
  --text-h1: 2.25rem;
  --text-h2: 1.75rem;
  --text-h3: 1.375rem;
  --text-h4: 1.125rem;
  --text-body: 1rem;
  --text-small: 0.875rem;
  --text-caption: 0.75rem;
  --text-code: 0.9375rem;
  --leading-tight: 1.2;
  --leading-snug: 1.35;
  --leading-normal: 1.65;
  --leading-relaxed: 1.75;

  /* Spacing */
  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-3: 0.75rem;
  --space-4: 1rem;
  --space-5: 1.25rem;
  --space-6: 1.5rem;
  --space-8: 2rem;
  --space-10: 2.5rem;
  --space-12: 3rem;
  --space-16: 4rem;
  --space-20: 5rem;
  --space-24: 6rem;

  /* Border Radius */
  --radius-sm: 6px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 24px;
  --radius-full: 999px;

  /* Shadows */
  --shadow-sm: 0 1px 3px rgba(0,0,0,0.06), 0 1px 2px rgba(0,0,0,0.04);
  --shadow-md: 0 4px 12px rgba(0,0,0,0.08), 0 2px 4px rgba(0,0,0,0.04);
  --shadow-lg: 0 8px 24px rgba(0,0,0,0.12), 0 4px 8px rgba(0,0,0,0.06);
  --shadow-xl: 0 16px 48px rgba(0,0,0,0.16), 0 8px 16px rgba(0,0,0,0.08);

  /* Transitions */
  --transition-fast: 0.15s ease;
  --transition-normal: 0.2s ease;
  --transition-slow: 0.3s ease;
  --transition-bounce: 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);

  /* Layout */
  --sidebar-width: 280px;
  --content-max-width: 900px;
  --content-wide-max-width: 1200px;
  --header-height: 60px;
  --z-sidebar: 100;
  --z-overlay: 200;
  --z-modal: 300;
  --z-toast: 400;
}

/* === DARK MODE === */
[data-theme="dark"] {
  --color-primary: #F07A68;
  --color-primary-dark: #E8614D;
  --color-primary-light: #3A2520;
  --color-secondary: #8BA0BD;
  --color-secondary-light: #6B84A0;
  --color-accent: #3DD6B0;
  --color-accent-dark: #2EC4A0;
  --color-accent-light: #1A3028;
  --color-bg: #1A1F26;
  --color-surface: #242B35;
  --color-surface-elevated: #2D3540;
  --color-border: #3A4450;
  --color-border-light: #323B46;
  --color-text-primary: #EAEAEA;
  --color-text-secondary: #A0A8B4;
  --color-text-tertiary: #6B7785;
  --color-text-inverse: #1A1A1A;
  --color-success-light: #1A3028;
  --color-warning-light: #332A14;
  --color-error-light: #331A1A;
  --color-nivel-c-bg: #1A3028;
  --color-nivel-b-bg: #332A14;
  --color-nivel-a-bg: #24203A;
  --gradient-hero: linear-gradient(135deg, #C94A36 0%, #1A2332 100%);
  --gradient-section: linear-gradient(135deg, #3A2520 0%, #1A3028 100%);
  --shadow-sm: 0 1px 3px rgba(0,0,0,0.2), 0 1px 2px rgba(0,0,0,0.15);
  --shadow-md: 0 4px 12px rgba(0,0,0,0.25), 0 2px 4px rgba(0,0,0,0.15);
  --shadow-lg: 0 8px 24px rgba(0,0,0,0.35), 0 4px 8px rgba(0,0,0,0.2);
}

/* === RESET === */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; -webkit-text-size-adjust: 100%; }
body {
  font-family: var(--font-body);
  font-size: var(--text-body);
  line-height: var(--leading-normal);
  color: var(--color-text-primary);
  background: var(--color-bg);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  overflow-x: hidden;
}
img { max-width: 100%; height: auto; display: block; }
a { color: var(--color-primary); text-decoration: none; transition: color var(--transition-fast); }
a:hover { color: var(--color-primary-dark); }
button { font-family: inherit; cursor: pointer; }
code { font-family: var(--font-mono); font-size: var(--text-code); }
::selection { background: var(--color-primary-light); color: var(--color-primary-dark); }

/* === ACCESSIBILITY === */
.skip-link {
  position: absolute;
  top: calc(-1 * var(--space-16));
  left: var(--space-4);
  background: var(--color-primary);
  color: var(--color-text-inverse);
  padding: var(--space-2) var(--space-4);
  border-radius: var(--radius-sm);
  z-index: calc(var(--z-toast) + 1);
  font-weight: 600;
}
.skip-link:focus { top: var(--space-4); }
.visually-hidden {
  position: absolute; width: 1px; height: 1px;
  padding: 0; margin: -1px; overflow: hidden;
  clip: rect(0,0,0,0); white-space: nowrap; border: 0;
}

/* === LAYOUT === */
.sidebar {
  position: fixed;
  top: 0; left: 0; bottom: 0;
  width: var(--sidebar-width);
  background: var(--color-secondary);
  color: var(--color-text-inverse);
  overflow-y: auto;
  z-index: var(--z-sidebar);
  display: flex;
  flex-direction: column;
  transition: transform var(--transition-slow);
}
.main {
  margin-left: var(--sidebar-width);
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
.overlay {
  position: fixed; inset: 0;
  background: rgba(0,0,0,0.5);
  z-index: calc(var(--z-sidebar) - 1);
  opacity: 0;
  pointer-events: none;
  transition: opacity var(--transition-slow);
}
.overlay--visible { opacity: 1; pointer-events: auto; }

/* === SIDEBAR === */
.sidebar-header {
  padding: var(--space-6) var(--space-5);
  border-bottom: 1px solid rgba(255,255,255,0.1);
}
.sidebar-brand {
  font-family: var(--font-heading);
  font-size: var(--text-h2);
  font-weight: 800;
  color: var(--color-primary);
  line-height: var(--leading-tight);
}
.sidebar-tagline {
  font-size: var(--text-small);
  opacity: 0.6;
  margin-top: var(--space-1);
}
.sidebar-progress {
  margin-top: var(--space-4);
}
.progress-bar {
  width: 100%;
  height: var(--space-2);
  background: rgba(255,255,255,0.15);
  border-radius: var(--radius-full);
  overflow: hidden;
}
.progress-fill {
  height: 100%;
  background: var(--color-accent);
  border-radius: var(--radius-full);
  transition: width var(--transition-slow);
  width: 0%;
}
.progress-text {
  font-size: var(--text-caption);
  opacity: 0.5;
  margin-top: var(--space-1);
  display: block;
}

/* Nav groups */
.nav-groups {
  flex: 1;
  padding: var(--space-3) 0;
  overflow-y: auto;
}
.nav-group { border-bottom: 1px solid rgba(255,255,255,0.05); }
.nav-group-toggle {
  display: flex; align-items: center; gap: var(--space-2);
  width: 100%;
  padding: var(--space-3) var(--space-5);
  background: none; border: none;
  color: rgba(255,255,255,0.85);
  font-family: var(--font-body);
  font-size: var(--text-small);
  font-weight: 600;
  text-align: left;
  transition: background var(--transition-fast);
  min-height: 44px; /* Touch target */
}
.nav-group-toggle:hover { background: rgba(255,255,255,0.06); }
.nav-group-icon { font-size: 1.1em; }
.nav-group-label { flex: 1; }
.nav-group-chevron {
  font-size: var(--text-caption);
  transition: transform var(--transition-normal);
  opacity: 0.5;
}
.nav-group--expanded .nav-group-chevron { transform: rotate(90deg); }
.nav-group-badge {
  font-size: var(--text-caption);
  background: rgba(255,255,255,0.1);
  padding: var(--space-1) var(--space-2);
  border-radius: var(--radius-full);
  opacity: 0.5;
}
.nav-group-items {
  max-height: 0;
  overflow: hidden;
  transition: max-height var(--transition-slow);
}
.nav-group--expanded .nav-group-items { max-height: 500px; }
.nav-item {
  display: flex; align-items: center; gap: var(--space-2);
  padding: var(--space-2) var(--space-5) var(--space-2) var(--space-10);
  color: rgba(255,255,255,0.65);
  font-size: var(--text-small);
  cursor: pointer;
  transition: all var(--transition-fast);
  border-left: 3px solid transparent;
  min-height: 44px; /* Touch target */
  text-decoration: none;
}
.nav-item:hover {
  color: var(--color-text-inverse);
  background: rgba(255,255,255,0.06);
}
.nav-item--active {
  color: var(--color-text-inverse);
  background: rgba(255,255,255,0.1);
  border-left-color: var(--color-primary);
  font-weight: 600;
}
.nav-item--visited::after {
  content: '✓';
  margin-left: auto;
  font-size: var(--text-caption);
  opacity: 0.4;
}

/* Sidebar footer */
.sidebar-footer {
  padding: var(--space-4) var(--space-5);
  border-top: 1px solid rgba(255,255,255,0.1);
}
.theme-toggle {
  display: flex; align-items: center; gap: var(--space-2);
  width: 100%;
  padding: var(--space-2) var(--space-3);
  background: rgba(255,255,255,0.08);
  border: none;
  color: rgba(255,255,255,0.8);
  font-size: var(--text-small);
  border-radius: var(--radius-md);
  transition: background var(--transition-fast);
  min-height: 44px;
}
.theme-toggle:hover { background: rgba(255,255,255,0.15); }

/* === TOPBAR === */
.topbar {
  position: sticky; top: 0;
  height: var(--header-height);
  background: var(--color-bg);
  border-bottom: 1px solid var(--color-border);
  display: flex; align-items: center; gap: var(--space-4);
  padding: 0 var(--space-6);
  z-index: calc(var(--z-sidebar) - 10);
}
.hamburger {
  display: none;
  width: 44px; height: 44px;
  background: none; border: none;
  flex-direction: column; justify-content: center; align-items: center; gap: 5px;
}
.hamburger-line {
  display: block;
  width: 22px; height: 2px;
  background: var(--color-text-primary);
  border-radius: var(--radius-full);
  transition: transform var(--transition-normal), opacity var(--transition-normal);
}
.hamburger--active .hamburger-line:nth-child(1) { transform: translateY(7px) rotate(45deg); }
.hamburger--active .hamburger-line:nth-child(2) { opacity: 0; }
.hamburger--active .hamburger-line:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }

/* Search */
.search-wrapper { flex: 1; max-width: 400px; position: relative; }
.search-input {
  width: 100%;
  padding: var(--space-2) var(--space-4);
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-full);
  font-family: var(--font-body);
  font-size: var(--text-small);
  color: var(--color-text-primary);
  outline: none;
  transition: border-color var(--transition-fast), box-shadow var(--transition-fast);
}
.search-input:focus {
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px var(--color-primary-light);
}
.search-results {
  display: none;
  position: absolute;
  top: calc(100% + var(--space-2));
  left: 0; right: 0;
  background: var(--color-surface-elevated);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-lg);
  max-height: 300px;
  overflow-y: auto;
  z-index: var(--z-overlay);
}
.search-results--visible { display: block; }
.search-result-item {
  padding: var(--space-3) var(--space-4);
  cursor: pointer;
  border-bottom: 1px solid var(--color-border-light);
  transition: background var(--transition-fast);
}
.search-result-item:hover { background: var(--color-primary-light); }
.search-result-item:last-child { border-bottom: none; }
.search-result-section { font-weight: 600; font-size: var(--text-small); }
.search-result-snippet {
  font-size: var(--text-caption);
  color: var(--color-text-secondary);
  margin-top: var(--space-1);
}
.search-highlight { background: var(--color-warning-light); padding: 0 2px; border-radius: 2px; }

/* === CONTENT SECTIONS === */
.section {
  flex: 1;
  animation: fadeSlideIn var(--transition-slow) ease;
}
.section[hidden] { display: none !important; }
.section-content { max-width: var(--content-max-width); margin: 0 auto; padding: var(--space-8) var(--space-6); }
.container { max-width: var(--content-max-width); margin: 0 auto; }

/* === HERO === */
.hero {
  background: var(--gradient-hero);
  color: var(--color-text-inverse);
  padding: var(--space-16) var(--space-6);
  margin: calc(-1 * var(--space-8)) calc(-1 * var(--space-6)) var(--space-8);
  text-align: center;
  border-radius: 0 0 var(--radius-xl) var(--radius-xl);
  position: relative;
  overflow: hidden;
}
.hero-title {
  font-family: var(--font-heading);
  font-size: 3rem;
  font-weight: 800;
  line-height: var(--leading-tight);
  text-shadow: 0 2px 12px rgba(0,0,0,0.25);
}
.hero-subtitle {
  font-size: var(--text-h3);
  opacity: 0.9;
  margin-top: var(--space-3);
}
.hero-quote {
  font-style: italic;
  opacity: 0.8;
  margin-top: var(--space-4);
  font-size: var(--text-body);
}
.hero-img {
  width: 100%;
  max-width: 600px;
  margin: var(--space-8) auto 0;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-xl);
}

/* Door cards */
.door-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: var(--space-4);
  margin-top: var(--space-8);
}
.door-card {
  background: var(--color-surface-elevated);
  border: 2px solid var(--color-border);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
  text-align: left;
  cursor: pointer;
  transition: transform var(--transition-normal), box-shadow var(--transition-normal), border-color var(--transition-normal);
  color: var(--color-text-primary);
}
.door-card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
}
.door-card--beginner { border-color: var(--color-accent); }
.door-card--beginner:hover { border-color: var(--color-accent-dark); }
.door-card--intermediate { border-color: var(--color-warning); }
.door-card--intermediate:hover { border-color: var(--color-primary); }
.door-card--advanced { border-color: var(--color-nivel-a-text); }
.door-card--advanced:hover { border-color: var(--color-primary); }
.door-card-emoji { font-size: var(--text-h1); }
.door-card-title {
  font-family: var(--font-heading);
  font-size: var(--text-h4);
  font-weight: 700;
  margin-top: var(--space-3);
}
.door-card-desc {
  font-size: var(--text-small);
  color: var(--color-text-secondary);
  margin-top: var(--space-2);
  line-height: var(--leading-normal);
}

/* === BREADCRUMB === */
.breadcrumb {
  font-size: var(--text-small);
  color: var(--color-text-tertiary);
  margin-bottom: var(--space-6);
  display: flex; align-items: center; gap: var(--space-2);
  flex-wrap: wrap;
}
.breadcrumb a { color: var(--color-text-secondary); cursor: pointer; }
.breadcrumb a:hover { color: var(--color-primary); }

/* === SECTION HERO IMAGE === */
.section-hero-img {
  width: 100%;
  border-radius: var(--radius-lg);
  margin-bottom: var(--space-8);
  box-shadow: var(--shadow-md);
  aspect-ratio: 16/9;
  object-fit: cover;
}

/* === TYPOGRAPHY (Content) === */
.section-content h1 {
  font-family: var(--font-heading);
  font-size: var(--text-h1);
  font-weight: 800;
  line-height: var(--leading-tight);
  letter-spacing: -0.02em;
  color: var(--color-primary);
  margin: 0 0 var(--space-4);
}
.section-content h2 {
  font-family: var(--font-heading);
  font-size: var(--text-h2);
  font-weight: 700;
  line-height: var(--leading-snug);
  letter-spacing: -0.01em;
  color: var(--color-text-primary);
  margin: var(--space-12) 0 var(--space-3);
  padding-bottom: var(--space-2);
  border-bottom: 2px solid var(--color-primary-light);
}
.section-content h2:first-child { margin-top: 0; }
.section-content h3 {
  font-family: var(--font-heading);
  font-size: var(--text-h3);
  font-weight: 700;
  line-height: var(--leading-snug);
  color: var(--color-secondary);
  margin: var(--space-8) 0 var(--space-2);
}
.section-content h4 {
  font-family: var(--font-heading);
  font-size: var(--text-h4);
  font-weight: 700;
  line-height: 1.4;
  margin: var(--space-6) 0 var(--space-2);
}
.section-content p {
  margin: 0 0 var(--space-4);
}
.section-content ul, .section-content ol {
  margin: 0 0 var(--space-4);
  padding-left: var(--space-6);
}
.section-content li { margin-bottom: var(--space-2); }
.section-content blockquote {
  border-left: 4px solid var(--color-primary);
  background: var(--color-primary-light);
  margin: var(--space-6) 0;
  padding: var(--space-4) var(--space-6);
  border-radius: 0 var(--radius-md) var(--radius-md) 0;
  font-style: italic;
  color: var(--color-text-secondary);
}
.section-content hr {
  border: none;
  border-top: 2px solid var(--color-border);
  margin: var(--space-10) 0;
}
.section-content code {
  font-family: var(--font-mono);
  font-size: var(--text-code);
  background: var(--color-surface);
  padding: var(--space-1) var(--space-2);
  border-radius: var(--radius-sm);
}
.section-content pre {
  background: var(--color-secondary);
  color: var(--color-text-inverse);
  padding: var(--space-4) var(--space-5);
  border-radius: var(--radius-md);
  overflow-x: auto;
  margin: var(--space-6) 0;
  white-space: pre-wrap;
  word-break: break-word;
}
.section-content pre code { background: none; color: inherit; padding: 0; }
.section-content strong { color: var(--color-text-primary); font-weight: 600; }
.section-content a { font-weight: 500; }
.section-content a:hover { text-decoration: underline; }
.section-content a[href^="http"]::after { content: " ↗"; font-size: 0.8em; }

/* === TABLES === */
.table-wrapper {
  overflow-x: auto;
  margin: var(--space-6) 0;
  border-radius: var(--radius-md);
  border: 1px solid var(--color-border);
}
.section-content table {
  width: 100%;
  border-collapse: collapse;
  font-size: var(--text-small);
}
.section-content th {
  background: var(--color-secondary);
  color: var(--color-text-inverse);
  font-weight: 600;
  padding: var(--space-3) var(--space-4);
  text-align: left;
  position: sticky; top: 0;
}
.section-content td {
  padding: var(--space-3) var(--space-4);
  border-bottom: 1px solid var(--color-border-light);
}
.section-content tr:nth-child(even) { background: var(--color-surface); }
.section-content tr:hover { background: var(--color-primary-light); }

/* === CALLOUT BOXES === */
.callout {
  padding: var(--space-4) var(--space-5);
  border-radius: var(--radius-md);
  margin: var(--space-6) 0;
  border-left: 4px solid;
  position: relative;
}
.callout-dato { background: var(--color-warning-light); border-color: var(--color-warning); }
.callout-prueba { background: var(--color-accent-light); border-color: var(--color-accent); }
.callout-avanzado { background: var(--color-nivel-a-bg); border-color: var(--color-nivel-a-text); }
.callout-importante { background: var(--color-primary-light); border-color: var(--color-primary); }

/* === ACCORDION === */
.accordion { margin: var(--space-4) 0; }
.accordion-header {
  display: flex; align-items: center; gap: var(--space-3);
  width: 100%;
  padding: var(--space-4) var(--space-5);
  background: var(--color-surface);
  border: 1px solid var(--color-border-light);
  border-radius: var(--radius-md);
  font-family: var(--font-heading);
  font-size: var(--text-h3);
  font-weight: 700;
  color: var(--color-secondary);
  cursor: pointer;
  transition: all var(--transition-normal);
  text-align: left;
  min-height: 44px;
}
.accordion-header:hover {
  background: var(--color-primary-light);
  border-color: var(--color-primary);
}
.accordion-header[aria-expanded="true"] {
  background: var(--color-primary-light);
  border-color: var(--color-primary);
  border-radius: var(--radius-md) var(--radius-md) 0 0;
}
.accordion-chevron {
  font-size: var(--text-caption);
  transition: transform var(--transition-normal);
  opacity: 0.5;
  margin-left: auto;
}
.accordion-header[aria-expanded="true"] .accordion-chevron { transform: rotate(90deg); }
.accordion-body {
  max-height: 0;
  overflow: hidden;
  transition: max-height var(--transition-slow);
  border: 1px solid var(--color-border-light);
  border-top: none;
  border-radius: 0 0 var(--radius-md) var(--radius-md);
}
.accordion-body--open {
  max-height: 10000px; /* Large enough for any content */
}
.accordion-body-inner {
  padding: var(--space-5);
}

/* === BADGES === */
.badge {
  display: inline-flex; align-items: center;
  font-size: var(--text-caption);
  font-weight: 600;
  padding: var(--space-1) var(--space-3);
  border-radius: var(--radius-full);
  white-space: nowrap;
}
.badge--nivel-c { background: var(--color-nivel-c-bg); color: var(--color-nivel-c-text); }
.badge--nivel-b { background: var(--color-nivel-b-bg); color: var(--color-nivel-b-text); }
.badge--nivel-a { background: var(--color-nivel-a-bg); color: var(--color-nivel-a-text); }
.badge--new { background: var(--color-accent-light); color: var(--color-accent-dark); }
.badge--done { background: var(--color-success-light); color: var(--color-accent-dark); }

/* === SECTION NAVIGATION (Prev/Next) === */
.section-nav {
  display: flex; justify-content: space-between; align-items: center;
  padding: var(--space-6);
  max-width: var(--content-max-width);
  margin: 0 auto;
  border-top: 2px solid var(--color-border);
  gap: var(--space-4);
}
.section-nav-prev, .section-nav-next {
  display: flex; align-items: center; gap: var(--space-2);
  padding: var(--space-3) var(--space-5);
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  font-size: var(--text-small);
  font-weight: 600;
  color: var(--color-text-primary);
  cursor: pointer;
  transition: all var(--transition-normal);
  text-decoration: none;
  min-height: 44px;
}
.section-nav-prev:hover, .section-nav-next:hover {
  background: var(--color-primary-light);
  border-color: var(--color-primary);
  color: var(--color-primary);
}
.section-counter {
  font-size: var(--text-caption);
  color: var(--color-text-tertiary);
}

/* === BACK TO TOP === */
.back-to-top {
  position: fixed;
  bottom: var(--space-6); right: var(--space-6);
  width: 48px; height: 48px;
  background: var(--color-primary);
  color: var(--color-text-inverse);
  border: none;
  border-radius: var(--radius-full);
  font-size: var(--text-h4);
  box-shadow: var(--shadow-md);
  opacity: 0;
  transform: translateY(var(--space-4));
  transition: opacity var(--transition-normal), transform var(--transition-normal);
  z-index: calc(var(--z-sidebar) - 20);
}
.back-to-top--visible { opacity: 1; transform: translateY(0); }

/* === FOOTER === */
.footer {
  padding: var(--space-8) var(--space-6);
  text-align: center;
  border-top: 1px solid var(--color-border);
  margin-left: var(--sidebar-width);
}
.footer-quote {
  font-style: italic;
  color: var(--color-text-secondary);
  font-size: var(--text-body);
  max-width: var(--content-max-width);
  margin: 0 auto var(--space-3);
  transition: opacity var(--transition-slow);
}
.footer-meta {
  font-size: var(--text-caption);
  color: var(--color-text-tertiary);
}

/* === CONFETTI CANVAS === */
.confetti-canvas {
  position: fixed; top: 0; left: 0;
  width: 100%; height: 100%;
  pointer-events: none;
  z-index: var(--z-toast);
}

/* === ANIMATIONS === */
@keyframes fadeSlideIn {
  from { opacity: 0; transform: translateY(var(--space-4)); }
  to { opacity: 1; transform: translateY(0); }
}
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
@keyframes scaleIn {
  from { opacity: 0; transform: scale(0.95); }
  to { opacity: 1; transform: scale(1); }
}
@keyframes slideUp {
  from { opacity: 0; transform: translateY(var(--space-8)); }
  to { opacity: 1; transform: translateY(0); }
}
@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}
@keyframes bounceIn {
  0% { opacity: 0; transform: scale(0.3); }
  50% { transform: scale(1.05); }
  70% { transform: scale(0.9); }
  100% { opacity: 1; transform: scale(1); }
}

/* Scroll-reveal utility (applied by JS) */
.reveal { opacity: 0; transform: translateY(var(--space-6)); transition: opacity var(--transition-slow), transform var(--transition-slow); }
.reveal--visible { opacity: 1; transform: translateY(0); }

/* === RESPONSIVE === */
@media (max-width: 480px) {
  .hero-title { font-size: var(--text-h1); }
  .hero-subtitle { font-size: var(--text-body); }
  .door-cards { grid-template-columns: 1fr; }
  .section-content { padding: var(--space-4); }
  .section-content h1 { font-size: 1.75rem; }
  .section-content h2 { font-size: 1.375rem; }
  .section-content h3 { font-size: 1.125rem; }
}

@media (max-width: 768px) {
  .sidebar { transform: translateX(-100%); }
  .sidebar--open { transform: translateX(0); }
  .main { margin-left: 0; }
  .hamburger { display: flex; }
  .footer { margin-left: 0; }
  .topbar { padding: 0 var(--space-4); }
  .section-nav { flex-direction: column; }
}

@media (min-width: 1024px) {
  .section-content { padding: var(--space-12) var(--space-8); }
}

@media (min-width: 1280px) {
  .section-content { padding: var(--space-12) var(--space-10); }
}

/* === PRINT === */
@media print {
  .sidebar, .topbar, .back-to-top, .hamburger, .overlay,
  .section-nav, .confetti-canvas, .footer, .theme-toggle,
  .sidebar-progress { display: none !important; }
  .main { margin-left: 0; }
  .section { display: block !important; page-break-inside: avoid; }
  .section[hidden] { display: block !important; }
  .accordion-body { max-height: none !important; }
  .section-content { max-width: 100%; padding: 0; }
  a { color: inherit; text-decoration: none; }
  a[href^="http"]::after { content: " (" attr(href) ")"; font-size: 0.8em; }
}
```

---

## 3. ⚡ JavaScript Architecture

### 3.1 Module Structure

All functions are defined at **global scope** (NOT inside try/catch — learned from v1 bug where onclick handlers couldn't find functions).

```javascript
// ============================================================
// SUENA v2 — JAVASCRIPT
// All functions at global scope for onclick accessibility
// ============================================================

// === DATA ===
var SECTION_ORDER = ['inicio', 'fundamentos-pulso', /* ...all 28 IDs... */];
var SECTION_LABELS = { 'inicio': '🏠 Inicio', 'fundamentos-pulso': '🎵 El Pulso', /* ... */ };
var SECTION_GROUPS = { 'fundamentos-pulso': 'fundamentos', /* ... */ };
var SECTION_TEXT = {};  // populated on init for search
var VISITED = {};       // populated from localStorage

// === NAVIGATION ===
function showSection(id) { /* ... */ }
function updateNav(id) { /* ... */ }
function updateBreadcrumb(id) { /* ... */ }
function updateSectionCounter(id) { /* ... */ }

// === SIDEBAR ===
function toggleSidebar() { /* ... */ }
function closeSidebar() { /* ... */ }
function toggleNavGroup(groupId) { /* ... */ }
function expandNavGroup(groupId) { /* ... */ }
function collapseAllNavGroups() { /* ... */ }

// === ACCORDIONS ===
function initAccordions() { /* ... */ }
function toggleAccordion(el) { /* ... */ }

// === SEARCH ===
function doSearch(query) { /* ... */ }

// === THEME ===
function toggleTheme() { /* ... */ }
function applyTheme(theme) { /* ... */ }

// === PROGRESS TRACKING ===
function markVisited(id) { /* ... */ }
function updateProgress() { /* ... */ }
function loadVisited() { /* ... */ }
function saveVisited() { /* ... */ }

// === SCROLL ANIMATIONS ===
function initScrollReveal() { /* ... */ }

// === CALLOUT DETECTION ===
function initCallouts() { /* ... */ }

// === TABLE WRAPPING ===
function initTables() { /* ... */ }

// === EXTERNAL LINKS ===
function initExternalLinks() { /* ... */ }

// === CONFETTI ===
function launchConfetti() { /* ... */ }
function checkGroupCompletion(groupId) { /* ... */ }

// === EASTER EGGS ===
function initEasterEggs() { /* ... */ }

// === FOOTER QUOTES ===
function initFooterQuote() { /* ... */ }
function rotateFooterQuote() { /* ... */ }

// === INIT ===
function init() {
  loadVisited();
  initCallouts();
  initAccordions();
  initTables();
  initExternalLinks();
  initScrollReveal();
  initEasterEggs();
  initFooterQuote();
  
  // Route from hash or default to inicio
  var hash = window.location.hash.slice(1);
  showSection(hash && document.getElementById('section-' + hash) ? hash : 'inicio');
  
  // Keyboard navigation
  document.addEventListener('keydown', handleKeyboard);
}

// Run init when DOM is ready
init();
```

### 3.2 Key Function Specs

#### showSection(id)
```
1. Hide all sections (set hidden attribute)
2. Show target section (remove hidden)
3. Apply fadeSlideIn animation (remove/add class)
4. Update sidebar nav (active state, expand group)
5. Update breadcrumb
6. Update section counter
7. Mark section as visited (localStorage)
8. Update progress bar
9. Scroll to top
10. Update URL hash
11. Close sidebar on mobile
12. Check group completion (confetti trigger)
```

#### initAccordions()
```
1. Find all H3 inside .section-content
2. For each H3:
   a. Collect all siblings until next H3 or H2 or end
   b. Wrap H3 in <button class="accordion-header" aria-expanded="false">
   c. Wrap siblings in <div class="accordion-body">
   d. First accordion open by default (aria-expanded="true")
   e. Accordions with 🚀 in the H3 text → always start collapsed + add badge "Avanzado"
3. Bind click events for toggle
```

#### initCallouts()
```
1. Find all <p> whose textContent starts with 💡, 🎯, 🚀, or ⚠️
2. Wrap each in appropriate .callout div:
   💡 → .callout.callout-dato
   🎯 → .callout.callout-prueba
   🚀 → .callout.callout-avanzado
   ⚠️ → .callout.callout-importante
3. Apply reveal class for scroll animation
```

#### Progress Tracking
```
localStorage key: "suena-visited"
Value: JSON array of section IDs
On visit: add to array, save, update progress bar
Progress: "X de 28" + width percentage
Group badges: "2/4" on sidebar groups
On complete group: launch confetti 🎉
```

---

## 4. 📝 Content Embedding Strategy

### 4.1 Pre-conversion Pipeline (Python)

```python
import markdown, os, base64

# 1. Convert all Markdown to HTML
md_extensions = ['tables', 'fenced_code', 'sane_lists', 'nl2br']
html_sections = {}
for file in markdown_files:
    html_sections[key] = markdown.markdown(content, extensions=md_extensions)

# 2. Convert images to base64
images_b64 = {}
for img_file in image_files:
    with open(img_path, 'rb') as f:
        b64 = base64.b64encode(f.read()).decode('utf-8')
    images_b64[name] = f'data:image/png;base64,{b64}'

# 3. Assemble HTML
# Each section becomes:
# <article class="section" data-section="{id}" id="section-{id}" hidden>
#   <div class="section-content container">
#     <nav class="breadcrumb">...</nav>
#     <img class="section-hero-img" src="{base64}" alt="..." loading="lazy">
#     {pre_rendered_html}
#   </div>
#   <nav class="section-nav">
#     <a class="section-nav-prev" data-prev="{prev_id}">← {prev_label}</a>
#     <span class="section-counter">{n} de 28</span>
#     <a class="section-nav-next" data-next="{next_id}">Siguiente: {next_label} →</a>
#   </nav>
# </article>
```

### 4.2 Image Assignment

| Section ID | Image | Alt Text |
|------------|-------|----------|
| inicio (hero) | hero.png | Adolescentes haciendo música juntos en un aula cálida |
| fundamentos-pulso | fundamentos.png | Ondas sonoras abstractas representando ritmo y pulso |
| voz-tecnica | coro.png | Adolescentes cantando juntos en un coro escolar |
| instrumento-guitarra | guitarra.png | Adolescente tocando guitarra acústica |
| instrumento-piano | piano.png | Adolescente descubriendo el piano |
| instrumento-bajo | bajo.png | Adolescente tocando bajo eléctrico |
| instrumento-percusion | percusion.png | Ensamble de percusión latina con bongós y cajón |
| ensamble | ensamble.png | Grupo completo de músicos adolescentes tocando juntos |
| creatividad-improvisacion | creatividad.png | Adolescentes componiendo y creando música |
| recursos-presentaciones | presentacion.png | Ensamble escolar en escenario con luces cálidas |

---

## 5. ♿ Accessibility Spec

| Requirement | Implementation |
|-------------|----------------|
| **Skip link** | `<a href="#main-content" class="skip-link">` |
| **Sidebar** | `role="navigation"`, `aria-label="Menú de navegación"` |
| **Hamburger** | `aria-label="Abrir menú"`, `aria-expanded="false/true"` |
| **Nav groups** | `aria-expanded` on toggle buttons |
| **Nav items** | `role="listitem"` inside `role="list"` |
| **Search** | `role="search"`, `aria-label="Buscar en el sitio"` |
| **Search results** | `role="listbox"`, items have `role="option"` |
| **Main content** | `role="main"`, `id="main-content"` |
| **Accordions** | `aria-expanded`, `aria-controls`, unique IDs |
| **Section nav** | `aria-label="Navegación de sección"` |
| **Theme toggle** | `aria-label="Cambiar tema"` |
| **Images** | `alt` text on ALL images, descriptive |
| **Back to top** | `aria-label="Volver arriba"` |
| **Touch targets** | Minimum 44x44px on all interactive elements |
| **Focus visible** | Clear focus ring on all focusable elements |
| **Keyboard** | Tab, Enter, Escape, Arrow keys for nav |
| **Contrast** | All text ≥ 4.5:1 (AA), headings ≥ 3:1 (AA-large) |

---

## 6. 📊 Metrics to Track

After the rebuild, these can be verified:

| Metric | Target |
|--------|--------|
| CSS custom properties used | 80/80 (100%) |
| Hardcoded px values | 0 |
| Touch targets ≥ 44px | 100% |
| ARIA attributes | All interactive elements |
| Animations/transitions | ≥ 20 unique |
| Accordions (auto-generated) | ~100+ from H3s |
| Callout boxes (auto-detected) | ~77 (💡🎯🚀⚠️) |
| Section navigation (prev/next) | 27 pairs |
| Progress tracking | 28 sections in localStorage |
| Easter eggs | ≥ 5 |
| File size (without images) | ~300 KB |
| File size (with base64 images) | ~15 MB |
