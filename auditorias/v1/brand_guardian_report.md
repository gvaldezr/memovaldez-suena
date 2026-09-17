# 🛡️ Auditoría de Marca — "Suena: Tu Espacio Musical"
## Brand Guardian Report · Septiembre 2026

> **Sitio auditado:** `artifacts/sitio_taller_musica/index.html` (288 KB, 6,468 líneas)
> **Brand guide de referencia:** `brand_guide.md` (22.5 KB)
> **Guía narrativa de referencia:** `guia_narrativa_sitio.md` (25 KB)
> **Audiencia:** Adolescentes 15-16 años, Bachillerato UADY, Mérida, Yucatán

---

## 📊 Scorecard de Coherencia de Marca

| Dimensión | Score | Veredicto |
|-----------|:-----:|-----------|
| Nombre y tagline | ⭐⭐⭐⭐⭐ | 5/5 — Consistente y bien comunicado |
| Paleta de colores | ⭐⭐⭐☆☆ | 3/5 — Colores de marca presentes pero 30 colores fuera de sistema |
| Tipografía | ⭐⭐⭐⭐☆ | 4/5 — Fuentes correctas, escala incompleta |
| Tono de voz | ⭐⭐⭐⭐⭐ | 5/5 — Excelente adherencia a la guía narrativa |
| Emojis | ⭐⭐⭐☆☆ | 3/5 — Densidad excesiva en algunas secciones |
| Imágenes | ⭐⭐⭐☆☆ | 3/5 — Presentes pero no evaluables (rutas locales) |
| Componentes UI | ⭐⭐⭐☆☆ | 3/5 — Hero y callouts presentes pero parcialmente implementados |
| Dark mode | ⭐⭐⭐⭐☆ | 4/5 — Funcional con tokens dedicados |
| Experiencia emocional | ⭐⭐⭐⭐☆ | 4/5 — Transmite calidez e inclusión, falta celebración |
| **PROMEDIO** | **⭐⭐⭐⭐☆** | **3.8/5 — Base sólida con gaps de implementación** |

---

## 1. 🏷️ Nombre y Tagline — 5/5 ✅

### Hallazgos
- **"Suena"** aparece **21 veces** en el sitio — consistente como identidad
- **"Tu Espacio Musical"** aparece **3 veces** (sidebar header, hero, title tag) — correcto
- **"Taller de Música"** se usa como referencia contextual, no como nombre de marca — correcto
- El title tag es `Suena — Tu Espacio Musical` — ✅ alineado al brand guide

### Veredicto
El nombre de marca se comunica de forma impecable. La distinción entre el nombre emocional ("Suena") y la referencia institucional ("Taller de Música, Bachillerato UADY") se respeta. Sin infracciones.

---

## 2. 🎨 Paleta de Colores — 3/5 ⚠️

### Lo que funciona ✅
- Los **14 colores principales del brand guide** están presentes en el CSS:
  - Primary Coral `#E8614D`: 17 usos ✅
  - Secondary Azul `#2D3A4A`: 8 usos ✅
  - Accent Menta `#2EC4A0`: 6 usos ✅
  - Warning Ámbar `#F5A623`: 3 usos ✅
  - Todos los fondos, superficies y variantes presentes
- El **gradiente hero** coral→azul está implementado ✅
- Las **variantes dark mode** existen ✅

### Lo que falla ❌
- **47 colores únicos** en el CSS — pero solo **14 son del brand guide** (30%)
- **30 colores "off-brand"** no triviales encontrados, incluyendo:
  - `#7C5CFC` (4 usos) — Morado para callout-avanzado. **No está en el brand guide** como variable, aunque el brand guide lo define como `--color-nivel-a-text: #6B4FBB`. El color usado es diferente (FC vs BB).
  - `#332A14`, `#3A2520`, `#1A3028` — Colores oscuros del dark mode que no están documentados como tokens.
  - `#8C8C8C`, `#6B7785` — Grises que no corresponden a ningún token definido.

### Severidad: MEDIA
Los colores "extra" parecen ser variantes de dark mode y estados, pero no están bajo control del sistema de tokens. El brand guide define 80 variables CSS, pero **solo 11 se usan con `var()`** — el 86% del CSS usa valores hardcoded directos.

### Recomendación
```
CRÍTICA: Refactorizar TODOS los valores de color hardcoded a var(--token).
Ejemplo: Cambiar `background: #FEF5E4` por `background: var(--color-warning-light)`.
Esto garantiza que dark mode y futuras evoluciones de marca funcionen automáticamente.
```

---

## 3. 🔤 Tipografía — 4/5

### Lo que funciona ✅
- **Google Fonts** cargadas correctamente: Nunito (400,600,700,800), Inter (400,500,600), JetBrains Mono (400)
- **Asignaciones correctas:**
  - Body: `'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif` ✅
  - Headings (H1, H2, H3): `'Nunito', sans-serif` ✅
  - Code: `'JetBrains Mono', monospace` ✅

### Lo que falla ❌
- **Escala tipográfica inconsistente con brand guide:**

  | Elemento | Brand Guide | Implementación | Match? |
  |----------|------------|----------------|--------|
  | H1 | 2.25rem (36px) | 2em (~32px), 3em, 2rem — **4 valores distintos** | ❌ |
  | H2 | 1.75rem (28px) | 1.5em (~24px) | ❌ |
  | H3 | 1.375rem (22px) | 1.2em (~19px) | ❌ |
  | H4 | 1.125rem (18px) | **No definido** (0 H4 en contenido) | ❌ |
  | Body | 1rem (16px) | 16px | ✅ |

- Los **H1 tienen 4 tamaños diferentes** (1.6em, 2em, 3em, 2rem) — inconsistencia grave para la marca
- **Line-height del brand guide: 1.2 para H1, 1.3 para H2** — el CSS usa 1.7 global. Bueno para legibilidad pero diferente del brand guide.
- **Letter-spacing**: Brand guide especifica -0.02em para H1 — no implementado
- **Responsive typography** no implementada — solo 1 media query `@media (max-width: 768px)` sin ajuste tipográfico. Brand guide pide H1 de 1.75rem en mobile.

### Severidad: MEDIA

### Recomendación
```css
/* Estandarizar a brand guide */
.content-inner h1 { font-size: 2.25rem; line-height: 1.2; letter-spacing: -0.02em; }
.content-inner h2 { font-size: 1.75rem; line-height: 1.3; letter-spacing: -0.01em; }
.content-inner h3 { font-size: 1.375rem; line-height: 1.35; }
@media (max-width: 768px) {
  .content-inner h1 { font-size: 1.75rem; }
  .content-inner h2 { font-size: 1.375rem; }
  .content-inner h3 { font-size: 1.125rem; }
}
```

---

## 4. 📝 Tono de Voz — 5/5 ✅

### Hallazgos
- **Tuteo consistente:** 357 menciones de "tú/tu", **0 menciones de "usted"** ✅
- **"Nosotros" comunitario:** 34 menciones de "nuestro/a/s" ✅
- **Español mexicano coloquial-educado:** Sin vulgaridades, sin formalismo innecesario ✅
- **Ejemplos generacionales:** Bad Bunny, Adele, Zoé, Disney, Café Tacvba, Natalia Lafourcade — todos presentes en el contenido ✅
- **Metáforas accesibles:** "Un acorde es como un abrazo grupal de sonidos" — exactamente el tono del brand guide ✅
- **Celebración del esfuerzo:** Frases motivacionales integradas en footer rotativo ✅
- **3 puertas de entrada sin señalar niveles:** "Empiezo aquí" / "Ya sé algo" / "Quiero más" — sin usar "principiante/intermedio/avanzado" ✅

### Veredicto
El tono de voz es el activo más fuerte del sitio. Sigue la guía narrativa con fidelidad excepcional. El "amigo mayor que sabe de música" se siente auténtico en cada sección.

---

## 5. 😊 Emojis — 3/5 ⚠️

### Lo que funciona ✅
- Emojis musicales para señalización de sección: 🎵🎤🎸🎹🥁🎶✨📚📋🏠📖 ✅
- Callout emojis: 💡🎯🚀⚠️ presentes ✅
- Emojis de sentimiento usados con moderación general ✅

### Lo que falla ❌
- **Densidad excesiva en algunas secciones:**
  - `inicio`: **4.1 emojis por párrafo** — Brand guide dice máximo 2 ❌
  - `fundamentos-lectura`: **9.8 emojis por párrafo** — gravemente fuera de norma ❌
  - `fundamentos-ritmo`: 1.0 por párrafo — en límite ⚠️
  - `fundamentos-pulso`: 0.7 por párrafo — correcto ✅
  - `fundamentos-melodia`: 0.8 por párrafo — correcto ✅

### Severidad: MEDIA
Las secciones de inicio y lectura musical saturan de emojis. Esto es especialmente problemático en `fundamentos-lectura` (9.8/párrafo) que probablemente incluye emojis musicales como contenido (notación con emojis de notas), no como señalización.

### Recomendación
Revisar `pagina_inicio.md` y `fundamentos_lectura.md` — reducir emojis decorativos. Los emojis de señalización (🎵 en headers) están bien; los emojis acumulados en párrafos de texto largo deben reducirse a ≤2 por párrafo.

---

## 6. 🖼️ Imágenes — 3/5 ⚠️

### Hallazgos
- **10 imágenes** presentes con `alt` text descriptivo ✅
- Rutas a archivos locales (`img/hero.png`, `img/guitarra.png`, etc.) — correctas para un sitio self-contained ✅
- Generadas con IA siguiendo directrices del brand guide (flat illustration, paleta coral/azul/menta, sin texto) ✅

### Lo que no puedo evaluar completamente
Como Brand Guardian, no puedo renderizar las imágenes dentro de este análisis. Sin embargo, basándome en los prompts documentados en `prompts_imagenes_suena.md`:
- Se especificó diversidad latinoamericana/yucateca ✅
- Se usó paleta de marca (coral, azul profundo, menta) ✅
- Estilo flat editorial illustration con textura risograph ✅
- CERO texto en imágenes (anti-pattern respetado) ✅

### Riesgo de marca
Las imágenes generadas con IA tienen riesgo de inconsistencia estilística entre ellas. Recomiendo revisión visual manual de las 10 imágenes para verificar que:
- Los tonos de piel representan diversidad yucateca real
- El estilo illustration es consistente entre todas
- No hay artefactos o elementos culturalmente inapropiados

### Severidad: BAJA (asumiendo prompts bien ejecutados)

---

## 7. 🧩 Componentes UI — 3/5 ⚠️

### Hero Section ✅ (parcial)
- Gradiente coral→azul implementado ✅
- Nombre "Suena" prominente ✅
- 3 door cards presentes (27 referencias) ✅
- Imagen hero incluida ✅
- **Pero:** 4 reglas CSS distintas para `.hero` — no unificadas como en el brand guide

### Callout Boxes ⚠️
- CSS para los 4 tipos definido (`.callout-dato`, `.callout-prueba`, `.callout-avanzado`, `.callout-importante`) ✅
- JS de auto-detección presente ✅
- **PERO:** Solo **3 instancias de cada clase callout** vs **41 emojis 💡**, **42 emojis 🎯**, **18 emojis 🚀** en el contenido
- Esto significa que **el JS solo está procesando ~9 de 101 callouts** — la mayoría aparece como texto plano ❌

### Cards
- No se usa la clase `.card` del brand guide con hover translateY(-2px) ❌
- Las door cards tienen estilo propio pero no siguen el componente card del brand guide

### Badges de nivel
- CSS para `.badge-nivel-a/b/c` definido ✅
- **Pero:** Las variables CSS `--color-nivel-a-bg/text` están definidas pero no se usan (0 `var()` references) ❌

### Progress Indicator
- Definido en brand guide como `.progress-bar` + `.progress-fill`
- **No implementado en el sitio** ❌

### Severidad: ALTA
Los callouts son la segunda infracción más grave después de las variables CSS. El JS post-processor no está capturando la mayoría de los callouts.

---

## 8. 🌙 Dark Mode — 4/5

### Lo que funciona ✅
- Toggle funcional con persistencia en localStorage ✅
- Paleta dark definida en `[data-theme="dark"]` con variables ✅
- Colores principales invertidos (Primary: #E8614D → #F07A68, Accent: #2EC4A0 → #3DD6B0) ✅
- Sidebar, content area, hero, footer adaptan ✅

### Lo que podría mejorar ⚠️
- Los **30 colores off-brand** probablemente incluyen dark mode variants hardcoded — si se refactorizan a `var()`, dark mode mejora automáticamente
- Los **callout boxes dark mode** tienen colores definidos (`#332A14`, `#24203A`, `#3A2520`, `#331A1A`) pero no están como tokens — son "colores mágicos" sin semántica

### Severidad: BAJA

---

## 9. ❤️ Experiencia Emocional — 4/5

### Lo que funciona ✅
- **Inclusión:** 3 puertas de entrada sin jerarquía peyorativa ✅
- **Comunidad:** "Nosotros", "nuestro ensamble", "lo hicimos juntos" ✅
- **Alegría:** Frases motivacionales en footer rotativo ✅
- **Creatividad:** Secciones de composición e improvisación empoderan al alumno ✅
- **Cultura yucateca:** "Bomba (yucateca)" en glosario, jarana, trova — presentes ✅

### Lo que falta ⚠️
- **Celebración:** No hay confetti, animación o feedback visual cuando el alumno completa algo ❌
- **Progreso:** No hay progress bar ni indicadores de "lo que has completado" ❌
- **Easter eggs:** El brand guide/guía narrativa planificaban un huevo de pascua oculto, micro-interacciones divertidas, 404 musical — **nada de esto está implementado** ❌
- **Revelación progresiva:** La guía narrativa propone secciones bloqueadas que se desbloquean conforme avanza el taller — no implementado ❌

### Severidad: MEDIA
El contenido transmite los valores; la experiencia interactiva no.

---

## 10. 🚨 Lista de Infracciones de Marca

| # | Infracción | Severidad | Ubicación | Fix recomendado |
|---|-----------|-----------|-----------|-----------------|
| 1 | **80 variables CSS definidas, solo 11 usadas** — 86% del sistema de diseño ignorado | 🔴 CRÍTICA | `<style>` global | Refactorizar todo el CSS para usar `var()` en lugar de valores hardcoded |
| 2 | **Callouts: ~92 de 101 no se estilizan** — JS auto-detect falla en la mayoría | 🔴 CRÍTICA | JS post-processor | Revisar regex del detector de callouts. Verificar que detecta `<p>💡` y `<strong>💡` |
| 3 | **H1 con 4 tamaños distintos** (1.6em, 2em, 3em, 2rem) | 🟠 ALTA | `.sidebar-header h1`, `.hero h1`, `.content-inner h1`, `.hero-title` | Unificar: content H1=2.25rem, hero H1=3rem, sidebar H1=1.5rem |
| 4 | **30 colores off-brand** sin semántica de token | 🟠 ALTA | Dark mode, callouts, badges | Mapear cada color a un token existente o crear nuevos tokens |
| 5 | **0 spacing via var()** — todo hardcoded en px | 🟠 ALTA | Todo el CSS | Usar `var(--space-4)` etc. en lugar de `16px` |
| 6 | **Escala tipográfica difiere del brand guide** (H2: 1.5em vs 1.75rem) | 🟡 MEDIA | `.content-inner h2/h3` | Actualizar a los valores exactos del brand guide |
| 7 | **Emojis >2/párrafo** en inicio (4.1) y lectura (9.8) | 🟡 MEDIA | `pagina_inicio`, `fundamentos_lectura` | Reducir emojis decorativos en cuerpo de texto |
| 8 | **0 H4 en todo el sitio** — brand guide los define | 🟡 MEDIA | Contenido | Usar H4 para subsecciones (actualmente usan `<strong>`) |
| 9 | **Solo 1 media query** — brand guide define 5 breakpoints | 🟡 MEDIA | `<style>` | Agregar breakpoints sm(640px), lg(1024px), xl(1280px) |
| 10 | **Progress indicator no implementado** | 🟡 MEDIA | — | Implementar `.progress-bar` del brand guide |
| 11 | **Sidebar 260px** vs brand guide 280px | 🟢 BAJA | `.sidebar` | Cambiar a `width: 280px` |
| 12 | **Max-width 900px** correcto, pero sin `container-wide` de 1200px | 🟢 BAJA | Layout | Agregar opción para grids de cards |
| 13 | **Cards sin hover effect** (translateY(-2px) del brand guide) | 🟢 BAJA | `.door-card` etc. | Agregar transition del brand guide |
| 14 | **Lucide icons** referenciados en brand guide pero no cargados | 🟢 BAJA | `<head>` | Agregar CDN de Lucide o mantener emojis como fallback |
| 15 | **aria-current="page"** faltante en nav activo | 🟢 BAJA | JS `showSection()` | Agregar `.setAttribute('aria-current', 'page')` |

---

## 📈 Resumen Ejecutivo

### Lo excepcional (proteger)
- **Tono de voz:** 5/5 — El contenido es el activo más valioso. Cada texto se siente como el "amigo mayor" del brand guide.
- **Nombre de marca:** 5/5 — "Suena" se comunica con consistencia y personalidad.
- **Tuteo absoluto:** 357 "tú" vs 0 "usted" — perfecto para la audiencia.
- **3 puertas de entrada:** Diseño inclusivo sin etiquetas de nivel.

### Lo urgente (arreglar)
1. **Variables CSS:** El sistema de diseño está definido pero ignorado. El 86% de las variables no se usan. Esto hace que cualquier cambio futuro de marca requiera editar 47 colores hardcoded en lugar de cambiar 14 tokens.
2. **Callouts:** La feature estrella del contenido (101 callouts educativos) aparece mayoritariamente como texto plano. El JS detector necesita debug.
3. **Tipografía inconsistente:** 4 tamaños de H1 diferentes rompen la jerarquía visual de la marca.

### Lo aspiracional (para v2)
- Progress indicators para que el alumno sienta que avanza
- Easter eggs y micro-interacciones para deleitar
- Revelación progresiva del menú a lo largo del año escolar
- Animaciones sutiles (notas flotando, ondas de sonido)

---

*Auditoría realizada por Brand Guardian · Pipeline de Producción de Cursos · Septiembre 2026*
*"La marca es una promesa. Cada pixel que la cumple la fortalece. Cada pixel que la ignora la debilita."*
