# 🎨 Auditoría UI Design — "Suena: Tu Espacio Musical"
## UI Designer Report · Septiembre 2026

> **Objeto:** Sitio HTML self-contained (~288 KB, 6,469 líneas, 28 secciones)
> **Brand Guide:** `brand_guide.md` (22.5 KB, 80+ tokens CSS definidos)
> **Análisis previo:** Visual Storyteller 3.1/5
> **Audiencia:** Adolescentes 15-16 años, Mérida, Yucatán

---

## 📊 Scorecard UI Design

| Dimensión | Puntuación | Veredicto |
|-----------|:----------:|-----------|
| Sistema de diseño | ⭐⭐⭐☆☆ | 3/5 — Tokens definidos pero 86% sin usar |
| Tipografía | ⭐⭐⭐☆☆ | 3/5 — Escala existe pero NO sigue el brand guide |
| Espaciado y ritmo | ⭐⭐☆☆☆ | 2/5 — 97 valores px hardcoded, sin sistema |
| Colores | ⭐⭐⭐⭐☆ | 4/5 — Paleta bien aplicada, 9 colores off-brand menores |
| Componentes UI | ⭐⭐⭐☆☆ | 3/5 — Callouts y cards existen pero faltan buttons, badges, progress |
| Sidebar/Navegación | ⭐⭐⭐☆☆ | 3/5 — Funcional pero touch targets insuficientes |
| Dark mode | ⭐⭐⭐⭐☆ | 4/5 — 28 variables, buena cobertura |
| Responsive | ⭐⭐⭐☆☆ | 3/5 — Solo 1 breakpoint, faltan tablet/desktop grande |
| Micro-interacciones | ⭐⭐☆☆☆ | 2/5 — 4 transitions, 5 hover states, 2 focus states |
| **PROMEDIO** | **⭐⭐⭐☆☆** | **3.0/5 — Infraestructura sólida, implementación inconsistente** |

---

## 1. 🧩 Sistema de Diseño — 3/5

### Hallazgo crítico: 86% de los tokens CSS están sin usar

El brand guide define **80 CSS custom properties** en `:root`. De estas, solo **11 se usan en el CSS** actual (14%). Las 69 restantes — incluyendo TODO el sistema de spacing (`--space-*`), border-radius (`--radius-*`), sombras (`--shadow-*`), transiciones (`--transition-*`), y tipografía (`--font-*`, `--text-*`, `--leading-*`) — están declaradas pero **nunca referenciadas con `var()`**.

```
Variables definidas: 80
Variables usadas:    11 (14%)
Variables perdidas:  69 (86%) ← PROBLEMA CENTRAL
```

**Variables usadas (las únicas 11):**
- `--color-bg`, `--color-border`, `--color-border-light`
- `--color-primary`, `--color-primary-dark`, `--color-primary-light`
- `--color-secondary`, `--color-surface`, `--color-surface-elevated`
- `--color-text-primary`, `--color-text-secondary`

**Variables NUNCA usadas (todas de spacing, radius, shadow, fonts):**
- `--space-1` a `--space-24` — TODAS perdidas
- `--radius-sm` a `--radius-xl` — TODAS perdidas
- `--shadow-sm` a `--shadow-xl` — TODAS perdidas
- `--font-heading`, `--font-body`, `--font-mono` — TODAS perdidas
- `--text-h1` a `--text-caption` — TODAS perdidas
- `--transition-fast` a `--transition-bounce` — TODAS perdidas

### Impacto
Sin un sistema de tokens conectado, el CSS es un **collage de valores hardcoded** que no puede mantener consistencia ni escalar. Cambiar un spacing requiere buscar y reemplazar en 97 instancias de `px`.

### Fix recomendado

```css
/* ANTES (actual) */
.content-inner h1 { font-size: 2em; margin: 0 0 16px; }
.content-inner h2 { font-size: 1.5em; margin: 32px 0 12px; }
.callout { padding: 16px 20px; border-radius: 12px; margin: 16px 0; }

/* DESPUÉS (conectado al sistema) */
.content-inner h1 { 
  font-family: var(--font-heading);
  font-size: var(--text-h1);
  line-height: var(--leading-tight);
  margin: 0 0 var(--space-4);
}
.content-inner h2 { 
  font-family: var(--font-heading);
  font-size: var(--text-h2);
  line-height: var(--leading-snug);
  margin: var(--space-8) 0 var(--space-3);
}
.callout { 
  padding: var(--space-4) var(--space-5);
  border-radius: var(--radius-md);
  margin: var(--space-4) 0;
}
```

**Esfuerzo:** ~2 horas de refactoring CSS. **Impacto:** ALTO — convierte el CSS de "collage" a "sistema de diseño".

---

## 2. 🔤 Tipografía — 3/5

### Google Fonts: ✅ Cargadas correctamente
Nunito, Inter y JetBrains Mono están referenciadas via `<link>` CDN con `preconnect`. La asignación es correcta:
- Headings → Nunito ✅
- Body → Inter ✅
- Code → JetBrains Mono ✅

### Escala tipográfica: ❌ No sigue el brand guide

| Elemento | Actual | Brand Guide | Delta |
|----------|--------|-------------|-------|
| H1 | 2em (32px) | 2.25rem (36px) | -4px ❌ |
| H2 | 1.5em (24px) | 1.75rem (28px) | -4px ❌ |
| H3 | 1.2em (19px) | 1.375rem (22px) | -3px ❌ |
| H4 | 1.05em (17px) | 1.125rem (18px) | -1px ⚠️ |
| Body | 16px | 1rem (16px) | ✅ |

Todos los headings son **más pequeños** que lo especificado en el brand guide. Esto reduce el contraste jerárquico — los H2 y H3 no se diferencian lo suficiente del body text.

### Line-height: ⚠️ Ligeramente desviado
- Body actual: `1.7` vs brand guide: `1.65`
- No se usan `--leading-tight` (1.2), `--leading-snug` (1.35), etc.

### H4: 0 instancias en HTML
El brand guide define H4 pero NO existe ningún `<h4>` en el contenido. Hay saltos directos de H3 a `<strong>`.

### Fix recomendado

```css
.content-inner h1 {
  font-family: var(--font-heading);
  font-size: var(--text-h1);       /* 2.25rem = 36px */
  font-weight: 800;
  line-height: var(--leading-tight); /* 1.2 */
  letter-spacing: -0.02em;
  margin: 0 0 var(--space-4);
  color: var(--color-primary);
}
.content-inner h2 {
  font-family: var(--font-heading);
  font-size: var(--text-h2);       /* 1.75rem = 28px */
  font-weight: 700;
  line-height: var(--leading-snug); /* 1.35 */
  letter-spacing: -0.01em;
  margin: var(--space-12) 0 var(--space-3); /* 48px top para más aire */
  padding-bottom: var(--space-2);
  border-bottom: 2px solid var(--color-primary-light);
}
.content-inner h3 {
  font-family: var(--font-heading);
  font-size: var(--text-h3);       /* 1.375rem = 22px */
  font-weight: 700;
  line-height: var(--leading-snug);
  margin: var(--space-8) 0 var(--space-2);
  color: var(--color-secondary);
}
```

---

## 3. 📐 Espaciado y Ritmo — 2/5

### 97 valores px hardcoded
El CSS tiene **97 instancias de valores en `px`** donde debería usar las variables `--space-*`. Los más frecuentes:

| Valor | Frecuencia | Equivalente token |
|-------|-----------|-------------------|
| 16px | 15x | `var(--space-4)` |
| 8px | 11x | `var(--space-2)` |
| 12px | 9x | `var(--space-3)` |
| 32px | 7x | `var(--space-8)` |
| 24px | 6x | `var(--space-6)` |
| 20px | 6x | `var(--space-5)` |

### Ritmo vertical insuficiente
- **H2 margin-top**: 32px — debería ser 48px (`--space-12`) para crear "respiración" entre bloques temáticos
- **H3 margin-top**: 24px — debería ser 32px (`--space-8`)
- **Entre secciones**: No hay separador visual entre secciones principales (Fundamentos → Voz → Instrumentos)
- **Callout margin**: 16px es insuficiente — los callouts deberían tener 24px de margin para destacar

### Border-radius inconsistente
| Valor | Frecuencia | Token correspondiente |
|-------|-----------|----------------------|
| 12px | 3x | `--radius-md` ✅ |
| 20px | 2x | No existe en brand guide ❌ |
| 8px | 2x | No existe en brand guide ❌ |
| 16px | 2x | `--radius-lg` ✅ |
| 4px | 1x | No existe en brand guide ❌ |
| 50% | 1x | Back-to-top ✅ |

La escala de radius del brand guide (`6px, 12px, 16px, 24px, 999px`) NO se respeta. Hay `20px`, `8px` y `4px` que no existen en el sistema.

### Fix recomendado
Buscar y reemplazar sistemáticamente todos los px hardcoded por tokens:

```css
/* Buscar y reemplazar */
padding: 16px     → padding: var(--space-4)
padding: 32px     → padding: var(--space-8)
margin: 24px 0    → margin: var(--space-6) 0
border-radius: 8px → border-radius: var(--radius-sm)
border-radius: 20px → border-radius: var(--radius-xl) /* o --radius-lg */
```

---

## 4. 🎨 Colores — 4/5

### Paleta bien aplicada
La tríada Coral + Azul + Menta se usa de forma coherente:
- **Coral (#E8614D)**: H1, links activos, primary accents — ✅ correcto
- **Azul Profundo (#2D3A4A)**: Sidebar, H3 — ✅ correcto
- **Menta (#2EC4A0)**: Callout prueba, badges — ✅ correcto

### 9 colores off-brand (menores)
| Color | Dónde | Debería ser |
|-------|-------|-------------|
| `#E8E8E8` | search input border | `var(--color-border)` (#E0DDD8) |
| `#FFF` / `#fff` | varios fondos | `var(--color-surface-elevated)` |
| `#f5f5f5` | code background | `var(--color-surface)` |
| `#f9f9f9` | table rows | `var(--color-surface)` |
| `#f0f0f0` | search results border | `var(--color-border-light)` |
| `#e0e0e0` | pre code color | `var(--color-text-secondary)` en dark |
| `#666` | text | `var(--color-text-secondary)` |
| `#1A2332` | gradient dark | OK — variante de dark mode |

Ninguno es grave, pero la suma de 9 colores fuera del sistema rompe la consistencia.

### Gradientes: ✅
`--gradient-hero` se usa correctamente en la hero section.

---

## 5. 🧱 Componentes UI — 3/5

### Lo que existe ✅

| Componente | Estado | Calidad |
|-----------|--------|---------|
| **Hero section** | ✅ Implementada | Gradiente + nombre + tagline + imagen |
| **Door cards (3)** | ✅ Implementadas | 3 cards con colores diferenciados |
| **Callout boxes (4 tipos)** | ✅ CSS + JS post-procesamiento | ~102 callouts detectables |
| **Tables** | ✅ 65 tablas | Headers coral, filas alternas |
| **Blockquotes** | ✅ 90 | Borde coral, fondo rosado |
| **Code blocks** | ✅ 60 | Fondo azul oscuro |
| **Footer rotativo** | ✅ | Frases motivacionales |
| **Imágenes** | ✅ 10 | Con alt text, rutas relativas |
| **Dark mode toggle** | ✅ | localStorage persistence |

### Lo que falta ❌

| Componente | Brand Guide | Implementado | Impacto |
|-----------|------------|-------------|---------|
| **Buttons (primary/secondary/ghost)** | ✅ Definidos | ❌ No existen | Alto — no hay CTAs |
| **Badges nivel A/B/C** | ✅ Definidos | ❌ No existen | Medio — diferenciación por nivel |
| **Progress bar** | ✅ Definido | ❌ No existe | Medio — gamificación |
| **Grid system (grid-3, grid-2)** | ✅ Definido | ❌ No existe | Medio — layout de cards |
| **Iconografía (Lucide)** | ✅ Recomendada | ❌ No cargada | Bajo — emojis compensan |

### Callout boxes — PROBLEMA SUTIL
El CSS y JS existen, pero hay un **problema potencial**: el JS detecta callouts buscando párrafos que empiecen con emojis (💡🎯🚀⚠️). Sin embargo, en el HTML pre-convertido de Markdown, los emojis pueden estar dentro de `<strong>` tags:

```html
<!-- Si el markdown era: **💡 Dato curioso:** -->
<!-- El HTML resultante podría ser: -->
<p><strong>💡 Dato curioso:</strong> texto...</p>
<!-- El JS busca textContent que empiece con 💡 — esto funciona -->
<!-- PERO si hay un <br> o salto antes del emoji, no matchea -->
```

Hay **102 emojis callout** en el contenido pero **0 `.callout` classes** en el HTML estático — el JS los crea dinámicamente. Si el JS falla o el orden de carga es incorrecto, los callouts quedan planos.

### Fix: Buttons faltantes

```css
.btn-primary {
  display: inline-block;
  background: var(--color-primary);
  color: var(--color-text-inverse);
  font-family: var(--font-body);
  font-weight: 600;
  font-size: var(--text-small);
  padding: var(--space-3) var(--space-6);
  border-radius: var(--radius-md);
  border: none;
  cursor: pointer;
  text-decoration: none;
  transition: background var(--transition-fast), transform 0.1s ease;
}
.btn-primary:hover {
  background: var(--color-primary-dark);
}
.btn-primary:active {
  transform: scale(0.98);
}
.btn-secondary {
  display: inline-block;
  background: transparent;
  color: var(--color-primary);
  border: 2px solid var(--color-primary);
  padding: calc(var(--space-3) - 2px) calc(var(--space-6) - 2px);
  border-radius: var(--radius-md);
  font-weight: 600;
  cursor: pointer;
  text-decoration: none;
  transition: background var(--transition-fast);
}
.btn-secondary:hover {
  background: var(--color-primary-light);
}
```

---

## 6. 📍 Sidebar/Navegación — 3/5

### Funcionalidad: ✅
- 28 secciones navegables
- Hamburger menu en mobile
- Active state con borde coral izquierdo
- Smooth scroll y hash routing

### Problemas

#### Touch targets insuficientes
Nav items tienen `padding: 8px 20px`. En mobile, esto resulta en un target de ~32px de alto — **debajo del mínimo WCAG de 44px**.

```css
/* Fix */
.nav-item {
  padding: 12px 20px; /* Mínimo 44px con line-height */
  min-height: 44px;
  display: flex;
  align-items: center;
}
.nav-item.sub {
  padding: 10px 20px 10px 36px;
  min-height: 44px;
}
```

#### Jerarquía visual de grupos plana
Los `.nav-group-label` tienen `opacity: 0.5` que los hace difíciles de leer. El contraste de `rgba(255,255,255,0.5)` sobre `#2D3A4A` es ~4:1 — borderline AA.

```css
/* Fix — más legible sin perder jerarquía */
.nav-group-label {
  opacity: 0.65; /* Sube de 0.5 */
  font-size: 0.7em;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  padding: var(--space-3) var(--space-5) var(--space-1);
  margin-top: var(--space-3);
}
```

#### Sin indicador de "sección actual" en URL
El hash cambia (`#fundamentos-pulso`) pero no hay feedback visual de que la URL se puede compartir/guardar.

---

## 7. 🌙 Dark Mode — 4/5

### Buena cobertura: 28 variables override
La paleta oscura es coherente: coral sube a `#F07A68`, fondo baja a `#1A1F26`, surface a `#242B35`.

### Problemas menores

#### Code blocks se confunden con el fondo
`background: var(--color-secondary)` (#2D3A4A) en light es perfecto, pero en dark mode el fondo general es `#1A1F26` y surface es `#242B35` — los code blocks con `#2D3A4A` apenas se distinguen.

```css
/* Fix */
[data-theme="dark"] .content-inner pre {
  background: var(--color-surface-elevated); /* #2D3540 — más contraste */
  border: 1px solid var(--color-border);
}
```

#### Callout dark mode backgrounds
Los colores dark de callouts (`#332A14`, `#1A3028`, `#24203A`, `#3A2520`) están definidos pero parecen estar en un segundo `[data-theme="dark"]` block. Verificar que se aplican correctamente y que el texto dentro es legible.

#### Table headers vibrantes en dark
Los th con `background: var(--color-primary)` (#F07A68 en dark) pueden ser muy vibrantes sobre fondo oscuro.

```css
[data-theme="dark"] .content-inner th {
  background: var(--color-secondary-light); /* Más sutil */
  color: var(--color-text-primary);
}
```

---

## 8. 📱 Responsive — 3/5

### Solo 2 media queries
```css
@media (max-width: 768px) { ... }  /* Mobile */
@media print { ... }                /* Impresión */
```

Falta:
- **640px** (tablet portrait) — las tablas y cards necesitan ajuste intermedio
- **1024px** (desktop) — breakpoint para sidebar behavior
- **1280px** (desktop grande) — el contenido de 900px max-width queda muy estrecho

### Tipografía responsive: ❌ No implementada
El brand guide especifica tamaños reducidos para mobile:
- H1: 2.25rem → 1.75rem en mobile
- H2: 1.75rem → 1.375rem en mobile
- H3: 1.375rem → 1.125rem en mobile

Esto NO está implementado.

### Fix

```css
@media (max-width: 768px) {
  .content-inner h1 { font-size: 1.75rem; }
  .content-inner h2 { font-size: 1.375rem; }
  .content-inner h3 { font-size: 1.125rem; }
  
  .hero-section h1 { font-size: 1.5rem; }
  .hero-section p { font-size: 1rem; }
  
  .door-cards { 
    grid-template-columns: 1fr; /* Stack en mobile */
    gap: var(--space-3);
  }
  
  .content-section {
    padding: var(--space-5) var(--space-4); /* 20px 16px */
  }
}

@media (min-width: 1280px) {
  .content-inner {
    max-width: 1000px; /* Un poco más ancho en pantallas grandes */
  }
}
```

---

## 9. ✨ Micro-interacciones — 2/5

### Inventario actual

| Tipo | Cantidad | Elementos |
|------|---------|-----------|
| **Hover states** | 5 | nav-item, theme-toggle, search-result, link, door-card |
| **Focus states** | 2 | search input, skip-to-content |
| **Transitions** | 4 | sidebar (0.3s), nav (0.2s), fade (0.3s), door-card (0.2s) |
| **Animations** | 1 | fadeIn al cambiar sección |

### Lo que falta

#### Focus-visible para navegación por teclado
No hay `:focus-visible` en ningún elemento. Usuarios de teclado no saben dónde están.

```css
*:focus-visible {
  outline: 2px solid var(--color-primary);
  outline-offset: 2px;
  border-radius: var(--radius-sm);
}
.nav-item:focus-visible {
  background: rgba(255,255,255,0.12);
  color: #fff;
  outline: 2px solid var(--color-primary);
  outline-offset: -2px;
}
```

#### Hover en imágenes de sección
Las 10 imágenes no tienen hover effect — una sutil scale o brightness haría que se sientan interactivas.

```css
.section-hero-img img {
  transition: transform var(--transition-slow);
}
.section-hero-img img:hover {
  transform: scale(1.02);
}
```

#### Transición entre secciones
Solo hay `fadeIn` (opacity + translateY). Se podría mejorar:

```css
@keyframes slideIn {
  from { opacity: 0; transform: translateY(12px); }
  to { opacity: 1; transform: translateY(0); }
}
.content-inner {
  animation: slideIn 0.35s cubic-bezier(0.16, 1, 0.3, 1);
}
```

#### Back-to-top button sin hover
```css
.back-to-top:hover {
  transform: scale(1.1);
  box-shadow: 0 6px 20px rgba(232, 97, 77, 0.4);
}
```

---

## 10. 📋 Recomendaciones Priorizadas con CSS

### 🔴 Prioridad 1 — Impacto Crítico

**1. Conectar los tokens CSS al stylesheet**
Refactorizar los 97 valores px hardcoded para usar `var(--space-*)`, `var(--radius-*)`, `var(--shadow-*)`. Esto es el fix de mayor impacto sistémico — convierte el CSS de collage a design system.

**2. Corregir escala tipográfica al brand guide**
H1 → 2.25rem, H2 → 1.75rem, H3 → 1.375rem. Agregar letter-spacing negativo en H1/H2 y line-heights del brand guide.

**3. Más "aire" vertical**
H2 margin-top → `var(--space-12)` (48px). Esto solo crea una separación visual enorme entre bloques temáticos — el contenido actual se siente comprimido.

### 🟡 Prioridad 2 — Impacto Alto

**4. Touch targets WCAG en sidebar**
Min-height 44px en todos los nav items. Crítico para mobile (90%+ del tráfico serán celulares de alumnos).

**5. Breakpoints responsive adicionales**
Agregar 640px y 1280px. Implementar tipografía responsive.

**6. Focus-visible global**
Para accesibilidad de teclado. 3 líneas de CSS.

**7. Buttons del brand guide**
Implementar `.btn-primary` y `.btn-secondary` — actualmente NO hay ningún CTA en todo el sitio excepto las door cards.

### 🟢 Prioridad 3 — Impacto Medio

**8. Dark mode refinements**
Code blocks, table headers, y callout backgrounds necesitan ajustes para mejor legibilidad.

**9. Micro-interacciones**
Image hover, back-to-top hover, nav focus-visible, transición mejorada entre secciones.

**10. Badges de nivel A/B/C**
Implementar inline en el contenido donde aplica. El CSS ya está en el brand guide.

---

## 🎯 Veredicto

### Score actual: 3.0/5

El sitio mejoró significativamente respecto al análisis previo (3.1/5 del Visual Storyteller, pero aquel medía dimensiones diferentes). Los avances principales son:

- ✅ Google Fonts cargadas
- ✅ Hero section con gradiente y door cards
- ✅ 10 imágenes con alt text
- ✅ Callout boxes CSS + JS detection
- ✅ Footer rotativo
- ✅ Skip-to-content
- ✅ ARIA básico (4 atributos)

Pero persiste un **problema sistémico**: el brand guide define un design system completo (80 tokens, componentes, escalas) que **no está conectado al CSS**. Es como tener un Stradivarius guardado en su estuche mientras se toca con un violín de juguete.

### La mejora transformadora #1

> **Refactorizar el CSS para usar `var()` en lugar de valores hardcoded.** Esto toma ~2-3 horas pero transforma la naturaleza del sitio de "HTML con estilos ad-hoc" a "producto con design system". Después de esto, todos los demás fixes (tipografía, spacing, responsive) se resuelven cambiando un solo valor en `:root` en lugar de buscar en 6,469 líneas.

### Analogía musical
> Si el brand guide es la partitura maestra, el CSS actual es como tener todas las notas escritas en un cuaderno suelto al lado del atril. Las notas son correctas, pero no están en la partitura — el director no puede señalar "compás 32" y que todos sepan qué tocar. Conectar los tokens es poner las notas EN la partitura. 🎵

---

*Reporte generado por UI Designer · Auditoría de Diseño · Pipeline de Producción de Cursos · Septiembre 2026*
