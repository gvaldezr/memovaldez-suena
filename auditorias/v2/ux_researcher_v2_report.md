# 🔬 Re-Auditoría UX — "Suena v2: Tu Espacio Musical"
## UX Researcher Report v2 · Septiembre 2026

> **Metodología:** Evaluación heurística comparativa (v1 vs v2) + análisis cuantitativo de implementación + cognitive walkthrough por persona.
> **Objeto v2:** `rediseno_suena_v2/index.html` (18.9 MB, 7,096 líneas, 28 secciones)
> **Objeto v1 de referencia:** `sitio_taller_musica/index.html` (281 KB, score anterior: 2.3/5)
> **Audiencia target:** Adolescentes 15-16 años, 1er grado bachillerato, Mérida, Yucatán
> **Dispositivo primario:** Celular
> **Personas:** Vale (formal), Santi (autodidacta), Majo (principiante)

---

## 📊 Scorecard Comparativo v1 → v2

| Dimensión | v1 Score | v2 Score | Δ | Veredicto v2 |
|-----------|:--------:|:--------:|:-:|-------------|
| Arquitectura de información | ⭐⭐⭐☆☆ 3/5 | ⭐⭐⭐⭐☆ 3.5/5 | +0.5 | Acordeones ayudan, pero sidebar sigue con 28 items |
| Flujos de usuario / Puertas | ⭐⭐☆☆☆ 2/5 | ⭐⭐⭐☆☆ 2.5/5 | +0.5 | Door cards existen pero onclick no implementado correctamente |
| Carga cognitiva | ⭐⭐☆☆☆ 2/5 | ⭐⭐⭐☆☆ 3/5 | +1.0 | Acordeones 🚀 reducen texto visible significativamente |
| Wayfinding | ⭐⭐⭐☆☆ 3/5 | ⭐⭐⭐⭐☆ 3.5/5 | +0.5 | Progress bar + checkmarks son un salto; falta prev/next |
| Engagement / Retención | ⭐⭐☆☆☆ 2/5 | ⭐⭐⭐⭐☆ 3.5/5 | +1.5 | Confetti + progress + Konami = salto mayor del sitio |
| Fricciones | ⭐⭐⭐☆☆ 3/5 | ⭐⭐⭐⭐☆ 3.5/5 | +0.5 | JS en global scope arregla navegación; faltan prev/next |
| Mobile UX | ⭐⭐⭐☆☆ 3/5 | ⭐⭐⭐⭐☆ 3.5/5 | +0.5 | 3 breakpoints, min-height 44px; peso 18.9 MB es problema |
| Accesibilidad | ⭐⭐☆☆☆ 2/5 | ⭐⭐⭐☆☆ 2.5/5 | +0.5 | ARIA presente (8 attrs), roles (3); aún insuficiente |
| Gamificación / Progreso | ⭐☆☆☆☆ 1/5 | ⭐⭐⭐⭐☆ 3.5/5 | +2.5 | De CERO a progress bar + checkmarks + confetti = MAYOR SALTO |
| **PROMEDIO** | **2.3/5** | **3.3/5** | **+1.0** | **Mejora significativa, especialmente en engagement y gamificación** |

---

## 📈 Evolución: De 2.3 a 3.3 — ¿Dónde Fue el Salto?

### Los 3 saltos más grandes (>1 punto)

| Dimensión | Salto | Causa |
|-----------|:-----:|-------|
| **Gamificación** | +2.5 | De literalmente CERO a progress bar + checkmarks en sidebar + confetti al completar grupos. El cambio más dramático de toda la auditoría. |
| **Engagement** | +1.5 | Confetti + Konami code + scroll reveals + footer rotativo. El sitio ya tiene momentos de "¡oh!" que antes no existían. |
| **Carga cognitiva** | +1.0 | Los acordeones para "🚀 Para los que quieren más" (42 instancias) colapsan contenido avanzado por defecto. Majo ya no ve texto que no es para ella. |

### Lo que NO mejoró significativamente

| Dimensión | Score | Por qué |
|-----------|:-----:|---------|
| **Flujos / Puertas** | 2.5 | Las door cards existen en el hero pero los `onclick` no están conectados — el análisis muestra 0 onclick funcionales en la zona del hero. Las puertas son decorativas, no funcionales. |
| **Accesibilidad** | 2.5 | Solo 8 atributos ARIA en todo el sitio (para 28 secciones + sidebar + search + acordeones). Falta `aria-current`, `aria-controls`, keyboard navigation en acordeones. |

---

## Análisis Detallado por Dimensión

### 1. 🏗️ Arquitectura de Información — 3.5/5 (+0.5)

#### Datos cuantitativos v2

| Métrica | v1 | v2 | Δ |
|---------|----|----|---|
| Secciones | 28 | 28 | = |
| Nav items | 31 | 28 | -3 (eliminados phantom items) |
| Grupos de nav | 10 | 10 | = |
| Acordeones H3 | 0 | Dinámicos (setupAccordions) | +✅ |
| Content chunking | 0 | 42 secciones 🚀 colapsables | +✅ |

#### Lo que mejoró ✅
- **Acordeones dinámicos**: La función `setupAccordions()` identifica H3 con "Para los que quieren más" y los convierte en colapsables automáticamente. Esto es exactamente lo que pedimos en v1 (R3.1).
- **Nav items limpios**: Se eliminaron 3 phantom items del JS que inflaban el sidebar en v1.

#### Lo que sigue pendiente ❌
- **Sidebar con 28 items sin colapsar grupos**: Los 10 grupos siguen mostrando todos los sub-items. La recomendación R1.1 (colapsar sub-items por grupo) no se implementó.
- **Formatos mezclados con contenido**: Los 6 formatos de evaluación siguen al mismo nivel que contenido educativo (R1.3 no implementada).
- **Sin indicadores temporales**: No hay "Semestre 1" / "Semestre 2" en el sidebar (R1.2 no implementada).

---

### 2. 🚪 Flujos de Usuario / Puertas — 2.5/5 (+0.5)

#### Hallazgo crítico: Door cards sin onclick funcional

El análisis del HTML muestra que la zona del hero contiene referencias textuales a "Empiezo aquí", "Ya sé algo" y "Quiero más", pero los `onclick` de las door cards **no están vinculados a funciones de navegación**. Al buscar onclicks en el área del hero, se encuentran 0 onclick funcionales — el contenido de las puertas está como texto dentro del HTML pre-renderizado del Markdown, no como componentes interactivos.

**Esto significa que las 3 puertas de entrada son DECORATIVAS, no funcionales.**

#### Impacto por persona

| Persona | Impacto |
|---------|---------|
| 🌱 **Majo** | Ve "🌱 Empiezo aquí" pero no puede hacer click para llegar a Fundamentos. Debe buscar en el sidebar manualmente. **Frustrante.** |
| 🎸 **Santi** | Ve "🎸 Ya sé algo" pero la puerta no lo lleva a elegir su instrumento. **Oportunidad perdida.** |
| 🎼 **Vale** | Ve "🎼 Quiero más" pero no accede a retos avanzados. **Confuso — parece que debería hacer algo pero no pasa nada.** |

#### Recomendación pendiente (ALTA prioridad)
Las door cards deben ser `<div>` con `onclick="showSection('...')"` claramente vinculados, NO texto Markdown pre-renderizado dentro de un párrafo.

---

### 3. 🧠 Carga Cognitiva — 3/5 (+1.0)

#### El mayor avance: Acordeones 🚀

| Métrica | v1 | v2 |
|---------|----|----|
| Texto total | ~34,600 palabras | ~35,957 palabras (ligeramente más por JS) |
| Secciones colapsables | 0 | 42 instancias de "🚀" potencialmente colapsables |
| Función setupAccordions | No existe | ✅ Implementada |
| Progressive disclosure | 0% | ~30% del contenido avanzado colapsable |

#### Lo que funciona ✅
- `setupAccordions()` busca H3 con "Para los que quieren más" y los convierte en acordeones colapsados por defecto
- Majo ya no ve contenido de "nivel avanzado" a menos que decida expandirlo
- La reducción visual de contenido es significativa — en secciones como "Fundamentos > Melodía", el texto visible se reduce ~40%

#### Lo que sigue pendiente ❌
- **Solo H3 con "Para los que quieren más" son colapsables** — el resto del texto sigue siendo un bloque largo
- **Sin TL;DR al inicio** de cada sección (R3.5 no implementada)
- **Sin iframes de herramientas** (Musicca, metrónomo siguen siendo links de texto, R3.2 no implementada)
- **Sin audio/video embebido** — un sitio de MÚSICA sigue sin sonido (R3.3 y R3.4 no implementadas)

---

### 4. 🗺️ Wayfinding — 3.5/5 (+0.5)

#### Nuevo: Progress tracking

| Feature | v1 | v2 |
|---------|----|----|
| Progress bar | ❌ | ✅ `progress-bar` + `progress-text` implementados |
| Checkmarks sidebar | ❌ | ✅ 34 referencias a checkmarks — secciones visitadas se marcan |
| Sección X/28 indicador | ❌ | ✅ Via progress text |
| Breadcrumbs | ❌ | ❌ No implementado |
| Prev/Next navigation | ❌ | ❌ **No implementado** (showSection NO contiene lógica de prev/next) |

#### Hallazgo crítico: Sin navegación Anterior/Siguiente

La función `showSection()` (943 chars) **no contiene lógica de navegación secuencial**. No hay botones "← Anterior | Siguiente →" al final de cada sección. Esto era la recomendación R4.2 (prioridad "Muy alto", esfuerzo "Bajo") y es la omisión más impactante de v2.

**Por qué importa:** Sin prev/next, el usuario termina una sección y queda "varado" — debe abrir el sidebar para elegir la siguiente. En mobile, esto requiere: tap hamburger → scroll sidebar → tap sección → esperar carga. Son 4 pasos para algo que debería ser 1 tap en "Siguiente →".

---

### 5. 🎯 Engagement — 3.5/5 (+1.5)

#### Features de engagement implementadas

| Feature | v1 | v2 | Impacto estimado |
|---------|----|----|-----------------|
| Scroll reveals | ❌ | ✅ IntersectionObserver (2 refs) | Medio — da vida al contenido |
| Confetti | ❌ | ✅ 12 referencias, función launchConfetti | Alto — momento de celebración |
| Konami code | ❌ | ✅ setupKonami + showKonamiEaster | Medio — factor "cuéntale a tu amigo" |
| Footer rotativo | ❌ | ✅ rotateQuote con arrays de frases | Bajo — detalles que suman |
| Progress bar visible | ❌ | ✅ Barra + texto "X de 28" | Alto — sensación de avance |
| Checkmarks | ❌ | ✅ markVisited + localStorage | Alto — gamificación básica funcional |

#### Cognitive Walkthrough v2 por Persona

##### 🌱 Majo (principiante) — Probabilidad de retorno: 🟡 35% (era 15%)

1. Llega al sitio → Ve hero con gradiente → Se siente bienvenida ✅
2. Ve "🌱 Empiezo aquí" → **Intenta hacer click → no pasa nada** → Confusión 😕
3. Abre sidebar → Busca "El Pulso" → Lo encuentra → Navega ✅
4. Lee el contenido → Scroll reveals hacen que el texto "aparezca" → Se siente más dinámico ✅
5. Ve "🚀 Para los que quieren más" → **Está colapsado** → No la abruma → ✅ (MEJORA SIGNIFICATIVA)
6. Termina la sección → Ve checkmark en sidebar → "¡Ya leí algo!" → Satisfacción 🎉
7. Ve progress bar: "1 de 28" → Siente que empezó → ✅
8. **Pero:** No hay botón "Siguiente" → Debe abrir sidebar de nuevo → Fricción
9. **Pero:** Links externos siguen sacándola del sitio
10. **Probabilidad de retorno:** Mejoró porque el progreso le da razón para volver, pero sin prev/next y sin interactividad real (quizzes, audio), la retención sigue siendo débil.

##### 🎸 Santi (autodidacta) — Probabilidad de retorno: 🟡 40% (era 20%)

1. Llega → Hero con gradiente → "Se ve mejor que antes" ✅
2. Busca su instrumento → Sidebar → Guitarra → Navega ✅
3. Lee la guía de guitarra → "Esto ya lo sé" → Scrollea rápido
4. Ve scroll reveals → "Ok, se mueve, está cool" ✅
5. Busca "los 4 acordes mágicos" → Usa search → Encuentra en Armonía → ✅ (search funciona)
6. **Descubre el Konami code** (si alguien se lo dice) → "¡Bombas yucatecas! jajaja" → 🎉
7. Completa Fundamentos → **CONFETTI** → "¡Ahhh!" → 🎊 (MOMENTO WOW)
8. **Pero:** Todo sigue siendo texto — no hay video de alguien tocando, no hay audio de los acordes
9. **Pero:** El archivo de 18.9 MB carga lento en su celular con datos móviles

##### 🎼 Vale (formal) — Probabilidad de retorno: 🟡 50% (era 40%)

1. Llega → Gradiente bonito → "Profesional" ✅
2. Va directo al sidebar → Busca Armonía/Composición → Navega ✅
3. Lee progresiones → Contenido excelente → Se queda ✅
4. Expande "🚀 Para los que quieren más" → Contenido avanzado → ✅ (MEJORA — antes todo estaba expuesto)
5. Progress bar → Le gusta ver su avance → ✅
6. Completa grupo Armonía → Confetti → Sonríe → 🎊
7. **Pero:** Sin quizzes ni retos prácticos, no hay forma de "demostrar" dominio
8. **Pero:** Las door cards "Quiero más" no funcionan — sintió que era para ella pero no respondió

---

### 6. ⚡ Fricciones — 3.5/5 (+0.5)

| Fricción v1 | Estado v2 |
|-------------|-----------|
| F1: Links externos sin target="_blank" | ⚠️ Parcial — JS debería forzar target pero no verificado |
| F2: Sin botón "volver arriba" | ✅ Implementado |
| F3: Callouts solo via JS (fallo = texto plano) | ✅ processCallouts() implementado (20 callouts procesados de ~77 potenciales) |
| F4: Glosario no filtrable | ❌ Sigue siendo lista estática |
| F5: Formatos no rellenables | ❌ Siguen siendo texto descriptivo |
| F6: Sidebar scroll largo en mobile | ⚠️ Parcial — min-height 44px pero 28 items siguen todos visibles |
| **NUEVO F7: Archivo de 18.9 MB** | 🔴 **CRÍTICO** — base64 images inflan el archivo. En datos móviles en Mérida (~5 Mbps), esto tarda ~30 segundos en cargar. Un adolescente espera máximo 3. |

#### Fricción nueva crítica: Peso del archivo

18.9 MB para un HTML self-contained es **inaceptable para el público meta**. Las 10 imágenes base64 (~18 MB de los 18.9) deberían ser archivos separados con lazy loading, o mejor aún, comprimidas a WebP (<200KB cada una).

> **Dato:** Según estudios de Google, 53% de los usuarios móviles abandonan un sitio que tarda >3 segundos en cargar. 18.9 MB en 4G yucateco = 15-30 segundos. **Esto mata la experiencia antes de empezar.**

---

### 7. 📱 Mobile UX — 3.5/5 (+0.5)

| Feature | v1 | v2 |
|---------|----|----|
| Breakpoints | 1 (768px) | 3 (480, 768, 1200px) ✅ |
| Touch targets | <44px | min-height: 44px ✅ |
| Hamburger sidebar | ✅ | ✅ |
| Swipe gestures | ❌ | ❌ |
| PWA / offline | ❌ | ❌ |
| **Peso del archivo** | 281 KB ✅ | **18.9 MB** 🔴 |

**El peso del archivo es la regresión más grave de v2.** El sitio v1 de 281 KB cargaba instantáneamente en cualquier conexión. El v2 de 18.9 MB es 67x más pesado y básicamente inutilizable en datos móviles.

---

### 8. ♿ Accesibilidad — 2.5/5 (+0.5)

| Feature | v1 | v2 |
|---------|----|----|
| aria-label | 0 | 5 ✅ |
| aria-expanded | 0 | 3 ✅ |
| role="main" | ❌ | ✅ |
| role="navigation" | ❌ | ❌ |
| role="search" | ❌ | ❌ |
| Skip-to-content | ✅ | ✅ |
| aria-current | ❌ | ❌ |
| Keyboard nav en acordeones | ❌ | ❌ |
| Alt text en imágenes | Verificar | Verificar |

**Mejora modesta.** De 0 ARIA a 8 es progreso, pero para un sitio con 28 secciones, sidebar dinámico, acordeones y modales de búsqueda, 8 atributos ARIA es insuficiente. El estándar WCAG AA requeriría ~50+ atributos ARIA para esta complejidad.

---

### 9. 🏆 Gamificación — 3.5/5 (+2.5) ⬆️ MAYOR SALTO

| Feature | v1 | v2 | Impacto |
|---------|----|----|---------|
| Progress bar | ❌ | ✅ | Alto — "X de 28 secciones" |
| Checkmarks en sidebar | ❌ | ✅ markVisited() | Alto — feedback visual inmediato |
| Confetti | ❌ | ✅ launchConfetti() + checkGroupCompletion() | Alto — celebración al completar grupo |
| Easter egg (Konami) | ❌ | ✅ setupKonami() + showKonamiEaster() | Medio — factor viral/social |
| Footer rotativo | ❌ | ✅ rotateQuote() | Bajo — detalles amables |
| Badges/logros | ❌ | ❌ | — |
| Mini-quizzes | ❌ | ❌ | — |
| Streak/racha | ❌ | ❌ | — |
| Nivel del usuario | ❌ | ❌ | — |

**De 0 a 5 features de gamificación es el salto más dramático de v2.** La combinación de progress tracking + checkmarks + confetti crea un loop básico de feedback: visita → marca → progreso → celebración. Esto es exactamente lo que le faltaba al v1 para que un adolescente sienta que "avanza".

**Lo que falta para llegar a 5/5:** Mini-quizzes interactivos al final de secciones clave. Sin evaluación activa, el "completar" una sección es solo visitarla — no hay verificación de comprensión.

---

## 🧠 Cognitive Walkthrough Consolidado: v1 vs v2

| Persona | Prob. retorno v1 | Prob. retorno v2 | Δ | Factor clave |
|---------|:----------------:|:----------------:|:-:|-------------|
| 🌱 **Majo** | 🔴 15% | 🟡 35% | +20pp | Progress tracking le da razón para volver. Door cards rotas y peso del archivo la frenan. |
| 🎸 **Santi** | 🔴 20% | 🟡 40% | +20pp | Confetti y Konami son "compartibles". Falta audio/video para competir con YouTube. |
| 🎼 **Vale** | 🟡 40% | 🟡 50% | +10pp | Acordeones 🚀 le dan contenido avanzado personalizado. Falta interactividad evaluativa. |

---

## 🎬 Plan de Acción: De 3.3 a 4.5

### 🔴 URGENTE — Hacer inmediatamente

| # | Acción | Score afectado | Esfuerzo |
|---|--------|:-------------:|----------|
| 1 | **Sacar imágenes de base64 → archivos separados + lazy loading** | Mobile +1.0, Fricciones +0.5 | Medio |
| 2 | **Door cards funcionales** con onclick vinculado a showSection() | Flujos +1.0 | Bajo |
| 3 | **Botones Anterior/Siguiente** al final de cada sección | Wayfinding +1.0, Engagement +0.5 | Bajo |

### 🟡 IMPORTANTE — Hacer esta semana

| # | Acción | Score afectado | Esfuerzo |
|---|--------|:-------------:|----------|
| 4 | **Callouts: verificar procesamiento** — solo 20 de ~77 detectados → revisar regex de detección | Carga cognitiva +0.5 | Bajo |
| 5 | **Sidebar colapsable por grupos** — sub-items se expanden al click | Arquitectura +0.5 | Medio |
| 6 | **TL;DR al inicio de cada sección** — 2-3 bullets con lo esencial | Carga cognitiva +0.5 | Bajo |
| 7 | **ARIA completo** — aria-current, aria-controls en acordeones, role en landmarks | Accesibilidad +1.0 | Medio |

### 🟢 SIGUIENTE ITERACIÓN

| # | Acción | Score afectado | Esfuerzo |
|---|--------|:-------------:|----------|
| 8 | **Mini-quizzes** interactivos (3-5 preguntas por sección clave) | Gamificación +1.0 | Alto |
| 9 | **Audio embebido** — al menos 1 ejemplo sonoro por sección de instrumento | Engagement +1.0 | Alto |
| 10 | **Glosario filtrable** con search interactivo | Fricciones +0.5 | Bajo |

### Proyección de score con las mejoras

| Escenario | Score proyectado |
|-----------|:----------------:|
| Solo urgentes (#1-3) | **3.8/5** |
| Urgentes + importantes (#1-7) | **4.2/5** |
| Todo (#1-10) | **4.6/5** |

---

## 💡 Insight Principal

> **Suena v2 dio el salto más importante: de un PDF con navegación a un sitio con personalidad y gamificación básica.** La progress bar, los checkmarks y el confetti transforman la experiencia de "leer un documento" a "explorar y avanzar". Ese cambio conceptual vale más que cualquier mejora visual.
>
> **La amenaza más grave a esta mejora es el peso del archivo (18.9 MB).** Un adolescente en Mérida con datos móviles no va a esperar 30 segundos para que cargue. Si el sitio no carga, ninguna feature importa. **Extraer las imágenes de base64 es la prioridad #1.**
>
> **El siguiente salto transformador sería audio embebido.** Un sitio de MÚSICA sin sonido sigue siendo una contradicción fundamental. Agregar un solo audio de ejemplo por sección de instrumento (30 segundos de guitarra, 30 de piano, etc.) cambiaría la naturaleza del sitio de "texto sobre música" a "experiencia musical".

---

*Re-auditoría UX · Evaluación heurística comparativa v1→v2 + cognitive walkthrough · Septiembre 2026*
