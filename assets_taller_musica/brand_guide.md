# 🎨 Brand Guide — Sitio Web del Taller de Música
## Bachillerato UADY · MEFI · 1er Grado

> **Este documento define la identidad visual completa del sitio web.**
> Todos los valores son finales y listos para implementar en CSS/HTML.
> Fecha: Septiembre 2026

---

## 1. Nombre del Sitio

### Opciones propuestas

| Opción | Nombre | Concepto | URL sugerida |
|--------|--------|----------|--------------|
| **A** | **Suena** | De la filosofía "La música es el vehículo" — algo que resuena, que suena, que vibra. Verbo activo. | suena.prepa.uady.mx |
| **B** | **Nuestro Ensamble** | Basado en comunidad — somos un ensamble, juntos sonamos | nuestroensamble.prepa.uady.mx |
| **C** | **TresSeis** | Referencia a 3/6 (compás ternario — vals, jarana yucateca) y a los 36 HCP del semestre 1. Inesperado, memorable, musical. | tresseis.prepa.uady.mx |

### ✅ Recomendación: **Suena**

**Por qué:**
- Corto (5 letras), memorable, pronunciable
- Funciona como verbo ("¿Cómo suena?"), como invitación ("¡Suena!") y como afirmación ("Suena bien")
- No es institucional — tiene personalidad propia
- Compatible con el tono del sitio: "Un amigo mayor que sabe mucho de música"
- El tagline natural sería: **"Suena — Tu espacio musical"**
- URL limpia: `suena.prepa.uady.mx`

**Nombre completo para documentos formales:** Taller de Música — "Suena" · Bachillerato UADY

---

## 2. Paleta de Colores

### Filosofía cromática

La paleta combina la **energía del coral/salmon** (calidez yucateca, vitalidad) con **azules profundos** (estructura musical, confianza) y **acentos de verde-menta** (frescura, juventud). Evita deliberadamente el rojo/negro rock y el dorado clásico — busca un espacio cromático que diga "moderno, inclusivo, vivo".

### Paleta principal

| Token | Color | HEX | Uso |
|-------|-------|-----|-----|
| **Primary** | Coral Cálido | `#E8614D` | Botones principales, links activos, elementos destacados |
| **Primary Dark** | Coral Intenso | `#C94A36` | Hover de primary, bordes activos |
| **Primary Light** | Coral Suave | `#FCEAE7` | Fondos de callouts, badges, highlights |
| **Secondary** | Azul Profundo | `#2D3A4A` | Headers, sidebar, texto sobre fondos claros |
| **Secondary Light** | Azul Medio | `#4A6078` | Texto secundario, iconos |
| **Accent** | Verde Menta | `#2EC4A0` | CTAs secundarios, éxito, progreso, badges "nuevo" |
| **Accent Dark** | Verde Menta Oscuro | `#22957A` | Hover de accent |
| **Accent Light** | Menta Suave | `#E6F9F4` | Fondos de sección "Prueba esto" |

### Fondos y superficies

| Token | Color | HEX | Uso |
|-------|-------|-----|-----|
| **Background** | Blanco Cálido | `#FAFAF8` | Fondo principal del sitio |
| **Surface** | Gris Nieve | `#F2F2EF` | Fondo de tarjetas, secciones alternas |
| **Surface Elevated** | Blanco | `#FFFFFF` | Tarjetas elevadas, modales |
| **Border** | Gris Suave | `#E0DDD8` | Bordes de tarjetas, separadores |
| **Border Light** | Gris Tenue | `#EDECEA` | Bordes sutiles, divisores dentro de tarjetas |

### Texto

| Token | Color | HEX | Contraste vs Background | Uso |
|-------|-------|-----|------------------------|-----|
| **Text Primary** | Casi Negro | `#1A1A1A` | 16.5:1 ✅ AAA | Títulos, texto principal |
| **Text Secondary** | Gris Oscuro | `#5C5C5C` | 7.2:1 ✅ AA | Subtítulos, descripciones |
| **Text Tertiary** | Gris Medio | `#8C8C8C` | 3.9:1 ✅ AA-large | Captions, metadata |
| **Text Inverse** | Blanco | `#FFFFFF` | — | Texto sobre fondos oscuros |

### Estados y feedback

| Token | Color | HEX | Uso |
|-------|-------|-----|-----|
| **Success** | Verde | `#2EC4A0` | (= Accent) Correcto, completado |
| **Success Light** | Verde Fondo | `#E6F9F4` | Fondo de mensajes de éxito |
| **Warning** | Ámbar | `#F5A623` | Atención, proceso, intermedio |
| **Warning Light** | Ámbar Fondo | `#FEF5E4` | Fondo de advertencias |
| **Error** | Rojo | `#E04848` | Error, incorrecto |
| **Error Light** | Rojo Fondo | `#FDECEC` | Fondo de errores |

### Gradientes

```css
/* Hero principal — Coral a Azul */
--gradient-hero: linear-gradient(135deg, #E8614D 0%, #2D3A4A 100%);

/* Sutil para headers de sección — Coral claro */
--gradient-section: linear-gradient(135deg, #FCEAE7 0%, #E6F9F4 100%);

/* Dark mode hero */
--gradient-hero-dark: linear-gradient(135deg, #C94A36 0%, #1A2332 100%);
```

### Dark Mode

| Token | Light | Dark |
|-------|-------|------|
| Background | `#FAFAF8` | `#1A1F26` |
| Surface | `#F2F2EF` | `#242B35` |
| Surface Elevated | `#FFFFFF` | `#2D3540` |
| Border | `#E0DDD8` | `#3A4450` |
| Text Primary | `#1A1A1A` | `#EAEAEA` |
| Text Secondary | `#5C5C5C` | `#A0A8B4` |
| Primary | `#E8614D` | `#F07A68` |
| Secondary | `#2D3A4A` | `#8BA0BD` |
| Accent | `#2EC4A0` | `#3DD6B0` |

---

## 3. Tipografía

### Fuentes seleccionadas (Google Fonts — gratuitas)

| Rol | Fuente | Peso | Razón |
|-----|--------|------|-------|
| **Headings** | **Nunito** | 700 (Bold), 800 (ExtraBold) | Redondeada, amigable, con personalidad pero legible. No es infantil — es acogedora. Perfecta para el tono "amigo mayor". |
| **Body** | **Inter** | 400 (Regular), 500 (Medium), 600 (SemiBold) | La fuente más legible en pantallas digitales. Diseñada para UI. Excelente para texto largo en celular. |
| **Accent / Código** | **JetBrains Mono** | 400 (Regular) | Monoespaciada moderna para: cifrado musical (C Am F G), tablaturas, nomenclatura, fragmentos de código. |

### Carga de fuentes

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400&family=Nunito:wght@700;800&display=swap" rel="stylesheet">
```

### Escala tipográfica

| Elemento | Fuente | Peso | Tamaño (rem) | Tamaño (px) | Line-height | Letter-spacing |
|----------|--------|------|-------------|-------------|-------------|----------------|
| **H1** | Nunito | 800 | 2.25 | 36 | 1.2 | -0.02em |
| **H2** | Nunito | 700 | 1.75 | 28 | 1.3 | -0.01em |
| **H3** | Nunito | 700 | 1.375 | 22 | 1.35 | 0 |
| **H4** | Nunito | 700 | 1.125 | 18 | 1.4 | 0 |
| **Body** | Inter | 400 | 1 | 16 | 1.65 | 0 |
| **Body Medium** | Inter | 500 | 1 | 16 | 1.65 | 0 |
| **Small** | Inter | 400 | 0.875 | 14 | 1.5 | 0.01em |
| **Caption** | Inter | 500 | 0.75 | 12 | 1.4 | 0.02em |
| **Code/Cifrado** | JetBrains Mono | 400 | 0.9375 | 15 | 1.6 | 0 |

### Responsive (Mobile)

En pantallas < 768px:
- H1: 1.75rem (28px)
- H2: 1.375rem (22px)
- H3: 1.125rem (18px)
- Body: 1rem (16px) — no reducir nunca

---

## 4. Iconografía y Emojis

### Familia de iconos: **Lucide**

Lucide es la familia recomendada por:
- Consistencia visual (línea fina, redondeada — combina con Nunito)
- Open source y gratuita
- Tiene iconos musicales relevantes (music, mic, headphones, guitar, etc.)
- Peso visual ligero — no compite con el contenido

```html
<script src="https://cdn.jsdelivr.net/npm/lucide-static@latest/lucide.min.js"></script>
```

### Iconos por sección

| Sección | Icono Lucide | Emoji alternativo |
|---------|-------------|-------------------|
| Inicio | `home` | 🏠 |
| Fundamentos | `music` | 🎵 |
| Nuestra Voz | `mic` | 🎤 |
| Instrumentos | `guitar` | 🎸 |
| Ensamble | `users` | 🎪 |
| Armonía | `layers` | 🎶 |
| Creatividad | `sparkles` | ✨ |
| Formatos | `clipboard-list` | 📋 |
| Recursos | `book-open` | 📚 |
| Glosario | `book-text` | 📖 |
| Presentaciones | `theater` | 🎭 |

### Uso de emojis

| Contexto | Emojis permitidos | Regla |
|----------|-------------------|-------|
| Títulos de sección | 🎵🎤🎸🎹🥁🎶✨📚📋🎪🏠📖🎭 | 1 emoji al inicio del título |
| Callout boxes | 💡🎯🚀⚠️✅ | 1 emoji por callout |
| Badges de nivel | 🌱🎸🎼 | 🌱 = Principiante, 🎸 = Autodidacta, 🎼 = Avanzado |
| En texto | 🎵🎶🤩😊🎉👏 | Máximo 2 por párrafo |
| **NUNCA** | 💀😤🤮👎😭 | Emojis negativos o agresivos |

---

## 5. Componentes UI

### Cards (Tarjetas)

```css
.card {
  background: var(--color-surface-elevated);
  border: 1px solid var(--color-border-light);
  border-radius: var(--radius-lg);           /* 16px */
  padding: var(--space-6);                    /* 24px */
  box-shadow: var(--shadow-sm);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}
.card:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-md);
}
```

### Buttons (Botones)

```css
/* Primary */
.btn-primary {
  background: var(--color-primary);
  color: var(--color-text-inverse);
  font-family: var(--font-body);
  font-weight: 600;
  font-size: 0.9375rem;
  padding: 0.75rem 1.5rem;
  border-radius: var(--radius-md);            /* 12px */
  border: none;
  cursor: pointer;
  transition: background 0.2s ease, transform 0.1s ease;
}
.btn-primary:hover {
  background: var(--color-primary-dark);
}
.btn-primary:active {
  transform: scale(0.98);
}

/* Secondary */
.btn-secondary {
  background: transparent;
  color: var(--color-primary);
  border: 2px solid var(--color-primary);
  padding: 0.625rem 1.375rem;
  border-radius: var(--radius-md);
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s ease;
}
.btn-secondary:hover {
  background: var(--color-primary-light);
}

/* Ghost */
.btn-ghost {
  background: transparent;
  color: var(--color-text-secondary);
  border: none;
  padding: 0.5rem 1rem;
  border-radius: var(--radius-sm);
  font-weight: 500;
  cursor: pointer;
}
.btn-ghost:hover {
  background: var(--color-surface);
  color: var(--color-text-primary);
}
```

### Badges / Tags

```css
/* Nivel de alumno */
.badge-nivel-c { /* 🌱 Principiante */
  background: #E6F9F4;
  color: #22957A;
  font-size: 0.75rem;
  font-weight: 600;
  padding: 0.25rem 0.75rem;
  border-radius: var(--radius-full);          /* 999px */
}
.badge-nivel-b { /* 🎸 Autodidacta */
  background: #FEF5E4;
  color: #B8820C;
}
.badge-nivel-a { /* 🎼 Avanzado */
  background: #EDE8FD;
  color: #6B4FBB;
}

/* Tipo de recurso */
.badge-lectura { background: #E8F4FD; color: #2A7AB5; }
.badge-video { background: #FDECF5; color: #B5397A; }
.badge-interactivo { background: #E6F9F4; color: #22957A; }
.badge-audio { background: #FEF5E4; color: #B8820C; }
```

### Callout Boxes

```css
.callout {
  padding: var(--space-5);                    /* 20px */
  border-radius: var(--radius-md);
  margin: var(--space-6) 0;
  border-left: 4px solid;
}

.callout-dato { /* 💡 Dato curioso */
  background: #FEF5E4;
  border-color: #F5A623;
}

.callout-prueba { /* 🎯 Prueba esto */
  background: #E6F9F4;
  border-color: #2EC4A0;
}

.callout-avanzado { /* 🚀 Para los que quieren más */
  background: #EDE8FD;
  border-color: #6B4FBB;
}

.callout-importante { /* ⚠️ Importante */
  background: #FCEAE7;
  border-color: #E8614D;
}
```

### Navegación Sidebar

```css
.sidebar {
  width: 280px;
  background: var(--color-secondary);         /* Azul Profundo */
  color: var(--color-text-inverse);
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  overflow-y: auto;
  padding: var(--space-6) 0;
  z-index: 100;
  transition: transform 0.3s ease;
}

.sidebar-link {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem 1.5rem;
  color: rgba(255,255,255,0.7);
  font-size: 0.9375rem;
  font-weight: 500;
  text-decoration: none;
  transition: all 0.2s ease;
  border-left: 3px solid transparent;
}
.sidebar-link:hover {
  color: #FFFFFF;
  background: rgba(255,255,255,0.08);
}
.sidebar-link.active {
  color: #FFFFFF;
  background: rgba(255,255,255,0.12);
  border-left-color: var(--color-primary);
  font-weight: 600;
}

/* Sub-items */
.sidebar-sublink {
  padding-left: 3rem;
  font-size: 0.875rem;
}

/* Mobile: hamburger menu */
@media (max-width: 768px) {
  .sidebar {
    transform: translateX(-100%);
  }
  .sidebar.open {
    transform: translateX(0);
  }
}
```

### Hero Section

```css
.hero {
  background: var(--gradient-hero);
  color: var(--color-text-inverse);
  padding: var(--space-16) var(--space-8);    /* 64px 32px */
  text-align: center;
  border-radius: 0 0 var(--radius-xl) var(--radius-xl);
  position: relative;
  overflow: hidden;
}
.hero h1 {
  font-size: 2.5rem;
  font-weight: 800;
  margin-bottom: var(--space-4);
  text-shadow: 0 2px 8px rgba(0,0,0,0.2);
}
.hero p {
  font-size: 1.25rem;
  opacity: 0.9;
  max-width: 600px;
  margin: 0 auto;
}
```

### Progress Indicator

```css
.progress-bar {
  width: 100%;
  height: 8px;
  background: var(--color-border);
  border-radius: var(--radius-full);
  overflow: hidden;
}
.progress-fill {
  height: 100%;
  background: var(--gradient-hero);
  border-radius: var(--radius-full);
  transition: width 0.5s ease;
}
```

---

## 6. Layout & Grid

### Max-width

```css
.container {
  max-width: 900px;        /* Contenido de lectura — óptimo para legibilidad */
  margin: 0 auto;
  padding: 0 var(--space-6);
}
.container-wide {
  max-width: 1200px;       /* Grids de tarjetas, dashboard */
  margin: 0 auto;
  padding: 0 var(--space-6);
}
```

### Grid

```css
/* Grid de tarjetas (3 puertas de entrada, instrumentos, etc.) */
.grid-3 {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: var(--space-6);
}

/* Grid de 2 columnas (comparaciones lado a lado) */
.grid-2 {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: var(--space-6);
}
```

### Breakpoints (Mobile-first)

| Breakpoint | Nombre | Tamaño | Descripción |
|------------|--------|--------|-------------|
| Default | Mobile | < 640px | 1 columna, sidebar oculta, padding reducido |
| `sm` | Tablet Portrait | ≥ 640px | 2 columnas posibles |
| `md` | Tablet Landscape | ≥ 768px | Sidebar visible |
| `lg` | Desktop | ≥ 1024px | Layout completo sidebar + contenido |
| `xl` | Desktop Grande | ≥ 1280px | Max-width alcanzado, centrado |

### Spacing Scale

```css
--space-1: 0.25rem;   /* 4px */
--space-2: 0.5rem;    /* 8px */
--space-3: 0.75rem;   /* 12px */
--space-4: 1rem;      /* 16px */
--space-5: 1.25rem;   /* 20px */
--space-6: 1.5rem;    /* 24px */
--space-8: 2rem;      /* 32px */
--space-10: 2.5rem;   /* 40px */
--space-12: 3rem;     /* 48px */
--space-16: 4rem;     /* 64px */
--space-20: 5rem;     /* 80px */
--space-24: 6rem;     /* 96px */
```

### Layout principal

```css
/* Desktop (≥ 768px) */
.layout {
  display: grid;
  grid-template-columns: 280px 1fr;
  min-height: 100vh;
}

/* Mobile */
@media (max-width: 767px) {
  .layout {
    grid-template-columns: 1fr;
  }
}
```

---

## 7. Imágenes & Ilustraciones

### Estilo visual: **Ilustración flat + fotografía documental**

| Tipo | Uso | Estilo |
|------|-----|--------|
| **Ilustraciones flat** | Iconos de sección, infografías, diagramas musicales | Colores de la paleta, líneas limpias, formas geométricas redondeadas |
| **Fotografía documental** | Hero, sección "Nuestras Presentaciones", galería | Natural, sin filtros extremos. Estudiantes reales haciendo música (cuando existan) |
| **Imágenes IA** | Decorativas para secciones sin foto real | Estilo ilustración semi-realista, musical, diverso, cálido |

### Directrices para imágenes IA

**✅ SÍ:**
- Instrumentos musicales en composición artística
- Ilustraciones abstractas de ondas sonoras, notas, ritmo
- Escenas de grupo diverso haciendo música (estilo ilustración, no fotorrealista)
- Naturaleza + música (elementos yucatecos: cenotes, haciendas, flora)
- Patrones y texturas musicales para fondos

**❌ NO:**
- **NUNCA texto dentro de la imagen** — todo texto va como overlay HTML/CSS
- Nunca personas fotorrealistas (derechos de imagen, uncanny valley)
- Nunca imágenes violentas, oscuras, o excluyentes
- Nunca estereotipos culturales (sombreros, sarapes cliché)

### Paleta de estilos de prompt para consistencia

```
ESTILO BASE: "Flat illustration, warm color palette with coral #E8614D and teal #2EC4A0 
accents, rounded shapes, clean lines, no text, white background, modern educational 
style, inclusive diverse characters"

VARIANTE MUSICAL: + "musical instruments, sound waves, musical notes floating"
VARIANTE YUCATÁN: + "tropical vegetation, cenote colors, Yucatan cultural elements, subtle"
VARIANTE ABSTRACTA: + "abstract sound visualization, geometric patterns, rhythm visualization"
```

### Tamaños de imagen

| Uso | Dimensiones | Formato |
|-----|-------------|---------|
| Hero | 1200 × 600 | WebP/PNG |
| Card thumbnail | 400 × 300 | WebP/PNG |
| Icono de sección | 200 × 200 | SVG preferido, PNG fallback |
| Infografía inline | 800 × auto | SVG preferido, PNG fallback |
| Avatar/perfil | 80 × 80 | PNG circular |

---

## 8. CSS Custom Properties (Variables)

```css
:root {
  /* ========================= */
  /* COLORES                   */
  /* ========================= */
  
  /* Primary — Coral Cálido */
  --color-primary: #E8614D;
  --color-primary-dark: #C94A36;
  --color-primary-light: #FCEAE7;
  
  /* Secondary — Azul Profundo */
  --color-secondary: #2D3A4A;
  --color-secondary-light: #4A6078;
  
  /* Accent — Verde Menta */
  --color-accent: #2EC4A0;
  --color-accent-dark: #22957A;
  --color-accent-light: #E6F9F4;
  
  /* Fondos */
  --color-bg: #FAFAF8;
  --color-surface: #F2F2EF;
  --color-surface-elevated: #FFFFFF;
  
  /* Bordes */
  --color-border: #E0DDD8;
  --color-border-light: #EDECEA;
  
  /* Texto */
  --color-text-primary: #1A1A1A;
  --color-text-secondary: #5C5C5C;
  --color-text-tertiary: #8C8C8C;
  --color-text-inverse: #FFFFFF;
  
  /* Estados */
  --color-success: #2EC4A0;
  --color-success-light: #E6F9F4;
  --color-warning: #F5A623;
  --color-warning-light: #FEF5E4;
  --color-error: #E04848;
  --color-error-light: #FDECEC;
  
  /* Badges de nivel */
  --color-nivel-c-bg: #E6F9F4;
  --color-nivel-c-text: #22957A;
  --color-nivel-b-bg: #FEF5E4;
  --color-nivel-b-text: #B8820C;
  --color-nivel-a-bg: #EDE8FD;
  --color-nivel-a-text: #6B4FBB;
  
  /* Gradientes */
  --gradient-hero: linear-gradient(135deg, #E8614D 0%, #2D3A4A 100%);
  --gradient-section: linear-gradient(135deg, #FCEAE7 0%, #E6F9F4 100%);
  --gradient-hero-dark: linear-gradient(135deg, #C94A36 0%, #1A2332 100%);
  
  /* ========================= */
  /* TIPOGRAFÍA                */
  /* ========================= */
  
  --font-heading: 'Nunito', system-ui, sans-serif;
  --font-body: 'Inter', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', 'Courier New', monospace;
  
  /* Tamaños */
  --text-h1: 2.25rem;
  --text-h2: 1.75rem;
  --text-h3: 1.375rem;
  --text-h4: 1.125rem;
  --text-body: 1rem;
  --text-small: 0.875rem;
  --text-caption: 0.75rem;
  --text-code: 0.9375rem;
  
  /* Line heights */
  --leading-tight: 1.2;
  --leading-snug: 1.35;
  --leading-normal: 1.65;
  --leading-relaxed: 1.75;
  
  /* ========================= */
  /* ESPACIADO                 */
  /* ========================= */
  
  --space-1: 0.25rem;    /* 4px */
  --space-2: 0.5rem;     /* 8px */
  --space-3: 0.75rem;    /* 12px */
  --space-4: 1rem;       /* 16px */
  --space-5: 1.25rem;    /* 20px */
  --space-6: 1.5rem;     /* 24px */
  --space-8: 2rem;       /* 32px */
  --space-10: 2.5rem;    /* 40px */
  --space-12: 3rem;      /* 48px */
  --space-16: 4rem;      /* 64px */
  --space-20: 5rem;      /* 80px */
  --space-24: 6rem;      /* 96px */
  
  /* ========================= */
  /* BORDES Y SOMBRAS          */
  /* ========================= */
  
  --radius-sm: 6px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 24px;
  --radius-full: 999px;
  
  --shadow-sm: 0 1px 3px rgba(0,0,0,0.06), 0 1px 2px rgba(0,0,0,0.04);
  --shadow-md: 0 4px 12px rgba(0,0,0,0.08), 0 2px 4px rgba(0,0,0,0.04);
  --shadow-lg: 0 8px 24px rgba(0,0,0,0.12), 0 4px 8px rgba(0,0,0,0.06);
  --shadow-xl: 0 16px 48px rgba(0,0,0,0.16), 0 8px 16px rgba(0,0,0,0.08);
  
  /* ========================= */
  /* TRANSICIONES               */
  /* ========================= */
  
  --transition-fast: 0.15s ease;
  --transition-normal: 0.2s ease;
  --transition-slow: 0.3s ease;
  --transition-bounce: 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
  
  /* ========================= */
  /* LAYOUT                    */
  /* ========================= */
  
  --sidebar-width: 280px;
  --content-max-width: 900px;
  --content-wide-max-width: 1200px;
  --header-height: 60px;
  
  /* ========================= */
  /* Z-INDEX                   */
  /* ========================= */
  
  --z-sidebar: 100;
  --z-overlay: 200;
  --z-modal: 300;
  --z-toast: 400;
}

/* ========================= */
/* DARK MODE                 */
/* ========================= */

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
```

---

## 9. Resumen Rápido — Cheatsheet

| Decisión | Valor |
|----------|-------|
| **Nombre** | Suena |
| **Tagline** | Tu espacio musical |
| **Primary** | Coral `#E8614D` |
| **Secondary** | Azul `#2D3A4A` |
| **Accent** | Menta `#2EC4A0` |
| **Font Heading** | Nunito 700/800 |
| **Font Body** | Inter 400/500/600 |
| **Font Mono** | JetBrains Mono 400 |
| **Iconos** | Lucide |
| **Border Radius** | 6 / 12 / 16 / 24px |
| **Max Width** | 900px (lectura) / 1200px (grid) |
| **Sidebar** | 280px, fondo Azul Profundo |
| **Breakpoint clave** | 768px (sidebar visible) |
| **Dark mode** | Sí, via `data-theme="dark"` |

---

*Brand Guide generada para el Taller de Música "Suena" — Bachillerato UADY MEFI*
*Septiembre 2026*
