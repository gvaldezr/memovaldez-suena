# 🎨 Análisis de Diseño Visual — "Suena: Tu Espacio Musical"
## Visual Storyteller Report · Septiembre 2026

> **Objeto de análisis:** Sitio web HTML self-contained (~280 KB, 28 secciones)  
> **Brand Guide de referencia:** `brand_guide.md` (22.5 KB)  
> **Guía Narrativa de referencia:** `guia_narrativa_sitio.md` (25 KB)  
> **Audiencia:** Adolescentes 15-16 años, Mérida, Yucatán  

---

## 📊 Scorecard General

| Dimensión | Puntuación | Veredicto |
|-----------|:----------:|-----------|
| Coherencia visual | ⭐⭐⭐☆☆ | 3/5 — Paleta definida pero poco implementada |
| Jerarquía visual | ⭐⭐⭐⭐☆ | 4/5 — Headings y spacing funcionales |
| Accesibilidad | ⭐⭐⭐☆☆ | 3/5 — Contraste OK, faltan ARIA y semántica |
| Engagement adolescente | ⭐⭐⭐☆☆ | 3/5 — Tono excelente, ejecución visual plana |
| Storytelling visual | ⭐⭐☆☆☆ | 2/5 — Arco narrativo no se refleja visualmente |
| Componentes UI | ⭐⭐☆☆☆ | 2/5 — Callouts y badges no implementados |
| Responsive/Mobile | ⭐⭐⭐⭐☆ | 4/5 — Sidebar/hamburger funcional, mobile-first |
| Dark mode | ⭐⭐⭐⭐☆ | 4/5 — 28 variables overridden, funcional |
| **PROMEDIO** | **⭐⭐⭐☆☆** | **3.1/5 — Estructura sólida, ejecución visual pendiente** |

---

## 1. 🎨 Coherencia Visual — 3/5

### Lo que funciona ✅

- **Paleta bien definida:** Coral `#E8614D` + Azul `#2D3A4A` + Menta `#2EC4A0` es una tríada cromática sólida — cálida, musical sin ser cliché, juvenil sin ser infantil.
- **Sidebar en Azul Profundo:** Crea un ancla visual consistente. El contraste con el fondo claro da estructura.
- **Headers en coral:** Los H1 en `#E8614D` son el elemento de marca más visible y consistente.
- **108 CSS variables definidas:** La infraestructura para consistencia está ahí.

### Lo que falla ❌

- **Solo 9 de 70+ variables CSS se usan realmente.** El brand guide define un sistema completo (spacing, radius, shadow, etc.) pero el CSS usa valores hardcoded. Esto rompe la escalabilidad y la consistencia.
- **Google Fonts NO cargan.** Nunito, Inter y JetBrains Mono están referenciados pero no hay `<link>` a Google Fonts (se eliminó junto con las CDN). El sitio cae a `-apple-system, BlinkMacSystemFont, Segoe UI, sans-serif` — una fuente genérica que pierde la personalidad de "Suena".
  - **Impacto:** ALTO. Nunito era la fuente de marca — sin ella, los headings pierden la calidez redondeada que conecta con adolescentes.
- **48 colores hex en el CSS**, muchos de los cuales son variantes no presentes en el brand guide (`#331A1A`, `#24203A`, `#332A14`). Probablemente del dark mode pero sin semántica.

### Recomendación

> **Prioridad ALTA:** Agregar Google Fonts como `<link>` (es un CDN confiable que funciona en todos los contextos, a diferencia de marked.js o Font Awesome). Sin Nunito, "Suena" pierde la mitad de su personalidad visual.
>
> Refactorizar el CSS para usar `var()` en lugar de valores hardcoded. Si el brand guide define `--space-6: 1.5rem`, el CSS debería decir `padding: var(--space-6)`, no `padding: 24px`.

---

## 2. 📐 Jerarquía Visual — 4/5

### Lo que funciona ✅

- **Escala tipográfica clara:** H1 (2em) → H2 (1.5em) → H3 (1.2em) → body (16px). Suficiente contraste entre niveles.
- **H2 con `border-bottom` en coral claro:** Excelente ancla visual para separar bloques temáticos. Se identifica rápido dónde empieza cada sección.
- **Max-width 900px:** Alineado con el brand guide. Longitud de línea óptima para lectura (~60-75 caracteres).
- **29 H1s, 200 H2s, 362 H3s:** Buena granularidad de contenido — no hay "muros de texto".

### Lo que podría mejorar 🟡

- **No hay H4.** El brand guide define `Nunito 700 / 1.125rem / 18px` para H4, pero el contenido salta de H3 a `<strong>`. Algunas subsecciones se beneficiarían de H4.
- **Spacing vertical entre secciones:** Actualmente `margin: 32px 0` en H2 y `24px 0` en H3. La guía sugiere `--space-12 (48px)` entre bloques temáticos mayores para dar más "respiración" — muy importante según la narrativa: *"Como en la música, los silencios importan."*
- **No hay visual separators** entre las grandes secciones (Fundamentos → Voz → Instrumentos). Todo fluye como un bloque continuo dentro de cada sección. Un divider decorativo (línea con emoji o SVG) daría ritmo visual.

---

## 3. ♿ Accesibilidad — 3/5

### Lo que funciona ✅

- **`lang="es"`:** Correcto para lectores de pantalla en español.
- **Viewport meta:** Mobile-first, buena base.
- **Contraste texto:** `#1A1A1A` sobre `#FAFAF8` = 16.5:1 (AAA). Excelente.
- **Tablas con `<th>` headers:** 181 headers tabulares — screen readers pueden navegar las tablas.
- **Line-height 1.7:** Muy buena legibilidad, especialmente en pantallas de celular.

### Lo que falla ❌

- **CERO atributos `aria-*`.** Ni `aria-label`, ni `aria-expanded` (para el hamburger), ni `aria-current` (para la navegación activa). Esto es un vacío significativo para usuarios de asistencia.
- **CERO atributos `role`.** El `<nav>` tiene semántica implícita, pero el sidebar toggle, search, y back-to-top deberían tener roles explícitos.
- **CERO imágenes, por lo tanto cero `alt` text.** Cuando se agreguen imágenes, CADA una necesita `alt` descriptivo.
- **Contraste en sidebar:** Texto `rgba(255,255,255,0.8)` sobre `#2D3A4A` = ~8.5:1 (AA). Pero el `.nav-group-label` con `opacity: 0.5` cae a ~4:1 — borderline.
- **No hay skip-to-content link** para navegación por teclado.
- **Tamaño mínimo de targets:** Los `.nav-item.sub` con `padding: 8px 20px` pueden ser muy pequeños en mobile (< 44x44px mínimo recomendado por WCAG).

### Recomendación

> **Prioridad MEDIA:** Agregar `aria-label` al hamburger, `aria-expanded` al sidebar toggle, `aria-current="page"` al nav activo, y un link invisible "Skip to content" al inicio.

---

## 4. 🎯 Engagement para Adolescentes — 3/5

### Lo que funciona ✅

- **El tono de voz es EXCELENTE.** Los textos siguen la guía narrativa fielmente: "Un amigo mayor que sabe de música." Las analogías son frescas ("Un acorde es como un abrazo grupal de sonidos"), los ejemplos son generacionales (Bad Bunny, Adele, Zoé, Disney), y el tuteo es natural.
- **26 "Dato curioso", 31 "Prueba esto", 20 "Para los que quieren más":** El contenido tiene variedad de formatos — no es un bloque monolítico de texto.
- **Emojis bien usados:** Emojis musicales para señalización (🎵🎤🎸🎹🥁), emojis emocionales con mesura (🤩😊🎉), nunca más de 2 por párrafo.
- **Easter eggs yucatecos** presentes: "Bomba (yucateca)" en glosario, jarana, trova.

### Lo que falla ❌

- **Visualmente se siente plano.** El texto es fantástico pero la EXPERIENCIA VISUAL es un muro de texto con headers de colores. Para un adolescente de 15 años acostumbrado a TikTok, Instagram y Spotify, esto se siente como un "documento largo", no como un "espacio musical".
- **CERO imágenes, ilustraciones o multimedia.** Ni una foto, ni un diagrama, ni una ilustración, ni un video embebido, ni un GIF. El brand guide habla de "flat illustration + fotografía documental" pero nada de esto existe.
- **Los callout boxes (💡🎯🚀) NO están estilizados.** Aparecen como texto plano con emoji — pero el brand guide define `.callout-dato` (fondo ámbar), `.callout-prueba` (fondo menta), `.callout-avanzado` (fondo morado). Sin los estilos, los callouts se pierden en el flujo de texto.
- **No hay hero section.** La página de inicio es texto plano, cuando debería ser un hero visual con gradiente coral→azul, nombre grande, y las 3 puertas de entrada como cards.
- **No hay micro-interacciones.** El brand guide menciona: loading musical, confetti al completar ejercicio, footer con frase rotativa, tooltip divertido en percusión. Nada de esto existe.
- **No hay "gamificación visual".** Sin badges, sin progress indicators, sin estados de "completado" — nada que haga al alumno sentir que avanza.

### Recomendación

> **Prioridad ALTÍSIMA:** Sin imágenes y sin callouts estilizados, el sitio no va a retener la atención de un adolescente. El tono de los textos compensa parcialmente, pero la experiencia visual necesita:
> 1. Hero section visual en la página de inicio
> 2. Callout boxes con colores del brand guide
> 3. Al menos 1 imagen/ilustración por sección
> 4. Cards para las 3 puertas de entrada

---

## 5. 📖 Storytelling Visual — 2/5

### Lo que funciona ✅

- **El arco narrativo está INCREÍBLEMENTE bien documentado** en la guía narrativa: Descubrimiento (S1-8) → Reto (S9-22) → Revelación (S23-28). Con curva emocional, metáforas, y cómo el sitio acompaña cada fase.
- **El concepto de "revelación progresiva del menú"** es una idea de diseño brillante — secciones que aparecen conforme avanza el taller, creando anticipación.

### Lo que falla ❌

- **NADA de esto se refleja visualmente en el sitio.** Las 28 secciones están todas visibles desde el inicio. No hay secciones bloqueadas, no hay indicadores de progreso, no hay banners de temporada (pre-navidad, pre-presentación final, cierre).
- **Las 3 puertas de entrada** (🌱 "Empiezo aquí" / 🎸 "Ya sé algo" / 🎼 "Quiero más") están como **texto plano** en la página de inicio en lugar de **3 cards visuales con colores diferenciados** (verde/azul/morado, como dice la guía).
- **No hay narrativas especiales** por momento clave (pre-Navidad, pre-final, cierre de año). La guía tiene textos bellísimos para cada uno, pero no hay mecanismo para mostrarlos.
- **No hay "Nuestras Presentaciones"** con multimedia — solo un placeholder de texto.

### Recomendación

> **Prioridad ALTA:** Implementar las 3 puertas como cards interactivas en el inicio. Aunque la revelación progresiva es difícil en un HTML estático, se pueden agregar secciones "Próximamente" con candado visual y texto de anticipación.

---

## 6. 🧩 Componentes UI — 2/5

### Lo que funciona ✅

- **65 tablas HTML** con `<th>` headers y styling alternado (filas pares con fondo gris). Las tablas de progresiones armónicas, figuras rítmicas y comparaciones son legibles.
- **Blockquotes** con borde izquierdo coral y fondo rosado — es el único componente "callout" que funciona bien visualmente.
- **Code blocks** con fondo azul oscuro y texto claro — buenos para mostrar cifrado musical y tablaturas.

### Lo que falla ❌

- **Callout boxes:** El brand guide define 4 tipos con colores distintos:
  - `💡 Dato curioso` → fondo ámbar `#FEF5E4`
  - `🎯 Prueba esto` → fondo menta `#E6F9F4`
  - `🚀 Para los que quieren más` → fondo morado `#EDE8FD`
  - `⚠️ Importante` → fondo coral `#FCEAE7`
  
  **NINGUNO está implementado.** Todos aparecen como párrafos normales con emoji. Esto es la brecha visual más impactante.

- **Badges de nivel (A/B/C):** El brand guide define `.badge-nivel-c` (verde), `.badge-nivel-b` (ámbar), `.badge-nivel-a` (morado). No existe ningún badge en el HTML.

- **Cards:** No hay ningún componente card en todo el sitio. Las 3 puertas de entrada, las guías de instrumentos, y las herramientas de recursos deberían presentarse como cards con hover effects.

- **Buttons:** Solo existe el toggle de dark mode como "botón". No hay CTAs con los estilos `btn-primary` / `btn-secondary` que define el brand guide.

- **Progress indicators:** No implementados. Un barra de progreso por sección o un "% completado" sería valioso para la gamificación.

### Recomendación

> **Prioridad ALTA:** Implementar callout boxes CSS es la mejora de mayor impacto-por-esfuerzo. Un regex que detecte `💡 **Dato curioso**`, `🎯 **Prueba esto**`, `🚀 **Para los que quieren más**` en el HTML y los envuelva en `<div class="callout callout-dato">` transformaría la experiencia visual.

---

## 7. 📱 Responsive / Mobile — 4/5

### Lo que funciona ✅

- **Sidebar oculta en mobile con hamburger:** `transform: translateX(-100%)` → `translateX(0)` con `.open`. Patrón correcto.
- **Overlay** para cerrar sidebar al tocar fuera — buena UX mobile.
- **Content padding reduce** de 32px a 16px en mobile.
- **Font-size base 16px** (nunca menor) — correcto para legibilidad mobile.
- **Max-width 900px** evita líneas demasiado largas en desktop.

### Lo que podría mejorar 🟡

- **Solo 2 media queries** (`max-width: 768px` para mobile y `@media print`). Falta:
  - Breakpoint de tablet (640px-768px): las tablas anchas se van a desbordar.
  - Breakpoint de desktop grande (1280px+): el contenido queda muy centrado y estrecho.
- **Tablas no son responsive.** Con 65 tablas, muchas de 4-5 columnas, en mobile van a requerir scroll horizontal. No hay `overflow-x: auto` en el contenedor de tablas.
- **Nav items mobile:** `padding: 8px 20px` puede ser muy pequeño como target táctil. WCAG recomienda mínimo 44x44px.

### Recomendación

> **Prioridad MEDIA:** Agregar `overflow-x: auto` a las tablas, y un breakpoint intermedio para tablet.

---

## 8. 🌙 Dark Mode — 4/5

### Lo que funciona ✅

- **28 variables CSS overridden** para dark mode — cobertura sólida.
- **Toggle funcional** con persistencia en `localStorage`.
- **Primary coral** sube a `#F07A68` en dark (más luminoso) — correcto para mantener visibilidad.
- **Background** baja a `#1A1F26` — oscuro sin ser negro puro (reduce fatiga visual).
- **Botón de toggle** en la sidebar con texto descriptivo.

### Lo que podría mejorar 🟡

- **Table headers en dark mode:** `background: var(--color-primary)` con `color: #fff` — funciona, pero en dark mode los headers coral sobre fondo oscuro pueden ser muy vibrantes. Considerar un tono más sutil.
- **Code blocks:** `background: var(--color-secondary)` (Azul Profundo `#2D3A4A`) se confunde con el fondo dark (`#1A1F26`). Debería usar `--color-surface-elevated` en dark.
- **Falta variable para blockquote background** en dark — el `#FCEAE7` coral claro sobre fondo oscuro creará un punto de alto contraste.

---

## 9. 🔍 Áreas de Mejora Generales

### Lo que le falta al sitio

| Elemento | Estado actual | Lo que debería tener | Impacto |
|----------|--------------|---------------------|---------|
| **Imágenes / Ilustraciones** | CERO | Al menos 1 por sección (~10 imágenes mínimo) | 🔴 Crítico |
| **Hero section visual** | Texto plano | Gradiente coral→azul, nombre grande, 3 cards | 🔴 Crítico |
| **Callout boxes estilizados** | Emoji + texto plano | 4 tipos con colores del brand guide | 🔴 Crítico |
| **Google Fonts** | No cargan | Link a Google Fonts CDN | 🔴 Crítico |
| **3 puertas como cards** | Lista de texto | Cards interactivas verde/azul/morado | 🟡 Alto |
| **Iconografía (Lucide)** | No carga | Iconos en sidebar y secciones | 🟡 Alto |
| **ARIA / accesibilidad** | Cero atributos | Labels, roles, skip-to-content | 🟡 Alto |
| **Tablas responsive** | Sin overflow | `overflow-x: auto` wrapper | 🟡 Alto |
| **Micro-interacciones** | Solo fadeIn | Hover en cards, tooltips, confetti | 🟢 Medio |
| **Progress indicators** | No existen | Barra de progreso por sección | 🟢 Medio |
| **Badges de nivel** | No existen | Tags A/B/C en contenido por nivel | 🟢 Medio |
| **Secciones bloqueadas** | Todas visibles | Revelación progresiva (candado visual) | 🟢 Medio |
| **Footer con frase rotativa** | No existe | Frase motivacional random del banco | 🟢 Medio |
| **404 musical** | No aplica (SPA) | — | ⚪ N/A |

---

## 10. 📋 Recomendaciones Priorizadas

### 🔴 Prioridad 1 — Impacto Crítico (hacer primero)

1. **Cargar Google Fonts.** Agregar `<link>` a Nunito + Inter + JetBrains Mono. Es CDN confiable y funciona en todos los contextos. Sin esto, la marca pierde identidad.

2. **Implementar callout boxes CSS.** Definir `.callout-dato`, `.callout-prueba`, `.callout-avanzado`, `.callout-importante` con los colores del brand guide. Aplicar via post-procesamiento del HTML (regex: detectar emoji → envolver en div).

3. **Crear hero section en página de inicio.** Reemplazar el H1 plano con un `<div class="hero">` que use `--gradient-hero`, nombre "Suena" grande, tagline, y las 3 puertas como cards debajo.

4. **Agregar al menos 8-10 imágenes/ilustraciones.** Generar con IA en estilo flat illustration (SIN texto en las imágenes). Prioridad:
   - Hero image: grupo de adolescentes haciendo música
   - Sección de cada instrumento: guitarra, piano, bajo, percusión
   - Ensamble: grupo tocando junto
   - Creatividad: manos componiendo/escribiendo
   - Presentación: escenario

### 🟡 Prioridad 2 — Impacto Alto

5. **Implementar las 3 puertas como cards.** Cards con borde de color, emoji grande, título, descripción breve, y link a la sección correspondiente.

6. **Tablas responsive.** Envolver cada `<table>` en `<div style="overflow-x:auto;">`.

7. **Accesibilidad básica.** Agregar `aria-label="Menú de navegación"` al hamburger, `aria-expanded` al sidebar, skip-to-content link.

8. **Usar CSS variables del brand guide.** Refactorizar `padding: 32px` → `padding: var(--space-8)`, etc.

### 🟢 Prioridad 3 — Impacto Medio

9. **Footer con frase motivacional rotativa.** Usar una del banco de 27 frases, seleccionada al azar al cargar.

10. **Badges de nivel** en el contenido por nivel (🌱/🎸/🎼 con colores).

11. **Progress indicator** sutil en el sidebar (puntos verdes en secciones visitadas).

12. **Micro-interacciones:** Hover en nav items (scale 1.02), transición más rica entre secciones, tooltip en iconos.

---

## 🎯 Veredicto Final

**El sitio tiene una base estructural sólida y un contenido editorial de altísima calidad.** Los 28 textos siguen la guía narrativa fielmente, el tono de voz conecta con la audiencia, y la arquitectura de información es clara.

**Sin embargo, la ejecución visual no está a la altura del contenido ni del brand guide.** El sitio se siente como un "documento formateado" más que como un "espacio musical". Las piezas para que sea espectacular ya existen (brand guide con 70+ variables, guía narrativa con storytelling, callout boxes definidos) — solo falta **implementarlas en el HTML/CSS**.

### Analogía musical
> Si el contenido es una partitura magistralmente compuesta, la implementación visual actual es como tocarla en un piano desafinado y sin pedal de sustain. Las notas están ahí, pero falta el **timbre, la dinámica y el color** que harían que suene como "Suena" debería sonar. 🎹

### Las 3 mejoras que transformarían el sitio:
1. **Google Fonts + callout boxes** = la marca cobra vida en 30 minutos de trabajo
2. **Hero visual + 3 puertas como cards** = la primera impresión cambia de "documento" a "experiencia"
3. **8-10 imágenes** = de "muro de texto" a "sitio web real"

---

*Reporte generado por Visual Storyteller · Pipeline de Producción de Cursos · Fase 6: Construcción de Assets · Septiembre 2026*
