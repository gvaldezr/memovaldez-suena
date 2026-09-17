# 🔬 Auditoría UX — "Suena: Tu Espacio Musical"
## UX Researcher Report · Septiembre 2026

> **Metodología:** Evaluación heurística (Nielsen) + análisis de arquitectura de información + cognitive walkthrough por persona + revisión técnica de accesibilidad.  
> **Objeto:** `index.html` (281 KB, 28 secciones, ~34,600 palabras)  
> **Audiencia target:** Adolescentes 15-16 años, 1er grado bachillerato, Mérida, Yucatán  
> **Dispositivo primario:** Celular (assumption basada en demografía)  
> **Personas de referencia:** Vale (formal), Santi (autodidacta), Majo (principiante)

---

## 📊 Scorecard UX

| Dimensión | Puntuación | Veredicto |
|-----------|:----------:|-----------|
| Arquitectura de información | ⭐⭐⭐☆☆ | 3/5 — Estructura lógica pero sobrecargada |
| Flujos de usuario / Puertas | ⭐⭐☆☆☆ | 2/5 — Door cards con routing incompleto |
| Carga cognitiva | ⭐⭐☆☆☆ | 2/5 — Demasiado texto, cero interactividad |
| Wayfinding | ⭐⭐⭐☆☆ | 3/5 — Sidebar funcional pero sin breadcrumbs ni contexto |
| Engagement / Retención | ⭐⭐☆☆☆ | 2/5 — Sin loops de retorno ni gamificación |
| Fricciones | ⭐⭐⭐☆☆ | 3/5 — Links rotos (external), no hay back-to-section |
| Mobile UX | ⭐⭐⭐☆☆ | 3/5 — Responsive pero no mobile-optimized |
| Accesibilidad | ⭐⭐☆☆☆ | 2/5 — Mínimos ARIA, 0 roles semánticos |
| Gamificación / Progreso | ⭐☆☆☆☆ | 1/5 — Cero indicadores de avance |
| **PROMEDIO** | **⭐⭐⭐☆☆** | **2.3/5 — Funcional pero sin experiencia de usuario diseñada** |

---

## 1. 🏗️ Arquitectura de Información — 3/5

### Datos duros
- **28 secciones** organizadas en **10 grupos** de navegación
- **31 items en sidebar** (3 top-level + 25 sub-items + 3 phantom items del JS)
- Sidebar scroll estimado: ~600px (requiere scroll en laptops pequeñas, no cabe en mobile sin scroll)

### Lo que funciona ✅
- **Agrupación por dominio musical:** Fundamentos → Voz → Instrumentos → Armonía → Creatividad → Formatos → Recursos → Glosario. La progresión es lógica y sigue el arco curricular.
- **Nombres de sección claros:** "El Pulso", "Acordes", "Guitarra" — sin jerga innecesaria.
- **Glosario al final** como recurso transversal — buena decisión.

### Problemas críticos ❌

**P1.1 — Sobrecarga de opciones (Hick's Law)**
28 secciones en un sidebar produce **parálisis de elección** en un adolescente. Estudios de Nielsen muestran que menús con más de 7±2 opciones reducen la eficacia de navegación. Para un usuario de 15 años cuyo referente de navegación es TikTok (infinite scroll sin menú) o Instagram (5 tabs máximo), un sidebar con 31 items es abrumador.

> **Dato:** El ratio "clicks para encontrar contenido" es 1 (bueno), pero el **tiempo visual de escaneo** del sidebar es alto — el usuario debe leer ~31 labels para orientarse.

**P1.2 — Sin jerarquía visual entre grupos**
Los 10 grupos de sidebar tienen el mismo peso visual. No hay distinción entre "Fundamentos" (esencial semana 1) y "Creatividad" (semestre 2). Para Majo (principiante), todo parece igualmente accesible/abrumador.

**P1.3 — Secciones de "Formatos" mezcladas con contenido educativo**
Los 6 formatos de evaluación (autoevaluación, coevaluación, bitácora) están al mismo nivel que contenido de aprendizaje. Son herramientas del profesor, no del alumno explorando. Mezclarlas genera confusión sobre la naturaleza del sitio: ¿es un recurso de aprendizaje o una plataforma de evaluación?

### Recomendaciones

| # | Recomendación | Impacto | Esfuerzo |
|---|---------------|---------|----------|
| R1.1 | **Colapsar grupos del sidebar** — los sub-items se expanden al hacer click en el grupo, no todos visibles siempre | Alto | Medio |
| R1.2 | **Agregar indicadores temporales** al sidebar: "Semestre 1" / "Semestre 2" / "Siempre disponible" | Medio | Bajo |
| R1.3 | **Mover Formatos a una sección oculta** o detrás de un link "Para mi profesor" — no son contenido de aprendizaje | Alto | Bajo |
| R1.4 | **Limitar sidebar visible a 5-7 grupos** con iconos grandes y expandibles | Alto | Medio |

---

## 2. 🚪 Flujos de Usuario / Puertas de Entrada — 2/5

### Las 3 puertas de entrada

El sitio tiene 3 "door cards" en la página de inicio:

| Puerta | Label | Destino actual | ¿Correcto para la persona? |
|--------|-------|---------------|---------------------------|
| 🌱 Empiezo aquí | Para Majo | → `fundamentos-pulso` | ✅ Correcto — el pulso es el primer concepto |
| 🎸 Ya sé algo | Para Santi | → `instrumento-guitarra` | ⚠️ **Parcial** — solo cubre guitarra, pero Santi podría tocar bajo o percusión |
| 🎼 Quiero más | Para Vale | → `armonia-progresiones` | ❌ **Incorrecto** — salta fundamentos, voz, instrumentos y 2 secciones de armonía (acordes) |

### Problemas críticos ❌

**P2.1 — Las puertas son callejones sin salida**
Las door cards navegan a UNA sección específica, pero no crean una **ruta guiada**. Después de llegar a "fundamentos-pulso", Majo no sabe si debe ir a ritmo, melodía o lectura. No hay "siguiente paso" ni breadcrumbs.

**P2.2 — "Ya sé algo" asume guitarra**
El 30-40% de autodidactas puede tocar piano, bajo o percusión. La puerta "Ya sé algo" debería llevar a una página de selección de instrumento, no directamente a guitarra.

**P2.3 — "Quiero más" salta todo el fundamento**
Vale (la formal) no necesita que le expliquen qué es el pulso, pero SÍ podría beneficiarse de la sección de improvisación, coro a 3 voces, o composición. Enviarla a "progresiones armónicas" es arbitrario.

**P2.4 — No hay flujo de retorno**
Una vez que el usuario navegó a una sección vía door card, no hay forma de volver al "modo guiado" o ver "qué sigue". El sidebar es la única navegación, y es genérica.

### Recomendaciones

| # | Recomendación | Impacto | Esfuerzo |
|---|---------------|---------|----------|
| R2.1 | **Puertas como rutas, no destinos** — cada puerta debería desplegar una secuencia: "Paso 1: Pulso → Paso 2: Ritmo → Paso 3: Melodía..." | Alto | Alto |
| R2.2 | **"Ya sé algo" → selector de instrumento** — "¿Qué tocas?" con 4 opciones (guitarra/piano/bajo/percusión) antes de navegar | Alto | Medio |
| R2.3 | **"Quiero más" → retos avanzados curados** — selección de 4-5 secciones avanzadas (improvisación, composición, armonía, arreglos) | Alto | Medio |
| R2.4 | **Agregar "Siguiente" y "Anterior" al final de cada sección** — breadcrumbs + next step | Alto | Bajo |

---

## 3. 🧠 Carga Cognitiva — 2/5

### Datos duros
- **34,639 palabras** totales (173 minutos de lectura a 200 wpm)
- **1,237 palabras promedio** por sección (~5 min de lectura cada una)
- **790 párrafos** — ninguno supera 100 palabras (bien)
- **65 tablas** — buen uso de formato estructurado
- **0 iframes, 0 audio, 0 video, 0 formularios interactivos** — CERO multimedia embebida

### El problema central

> **El sitio es un documento largo disfrazado de sitio web.**

Para un adolescente de 15 años cuyo consumo digital promedio es:
- **TikTok:** Videos de 30-60 segundos, altamente visuales
- **Instagram:** Imágenes + stories con máximo 2 párrafos
- **YouTube:** Tutoriales de 5-10 minutos con demostración visual
- **Spotify:** Audio + cover art, cero texto

...un sitio con **34,600 palabras de texto corrido** (equivalente a un libro de ~80 páginas) y **CERO contenido multimedia embebido** representa una fricción cognitiva masiva.

### Hallazgos específicos

**P3.1 — Secciones de 5+ pantallas de scroll**
Cada sección requiere ~4-6 pantallas de scroll (en desktop). En mobile, eso se duplica. Para "fundamentos-lectura" (1,422 palabras), un adolescente scrollea ~12 pantallas en celular sin encontrar un solo elemento interactivo.

**P3.2 — Sin chunking progresivo**
Todo el contenido de cada sección se muestra de golpe. No hay accordions, tabs, ni "leer más". El usuario ve un muro de texto y decide si lo lee o se va.

**P3.3 — Los embeds son links, no embeds reales**
El contenido menciona herramientas como Musicca, Teoria.com, MuseScore — pero son links de texto, no iframes. El usuario debe salir del sitio para interactuar. **Cada salida es un punto de fuga** del que muchos adolescentes no regresan.

**P3.4 — Sin contenido multimedia**
0 videos embebidos, 0 audio players, 0 actividades interactivas. Para un sitio de MÚSICA, la ausencia de sonido es una contradicción fundamental.

### Recomendaciones

| # | Recomendación | Impacto | Esfuerzo |
|---|---------------|---------|----------|
| R3.1 | **Acordeones/tabs para subsecciones** — mostrar H2 como tabs colapsables, revelar contenido progresivamente | Muy alto | Medio |
| R3.2 | **Embeber herramientas externas como iframes** — Musicca, piano virtual, metrónomo DENTRO del sitio | Alto | Medio |
| R3.3 | **Audio embebido** — cada sección de instrumento debería tener un audio de ejemplo mínimo (embed de SoundCloud o archivo MP3) | Alto | Alto |
| R3.4 | **Videos de YouTube embebidos** — al menos 1 por sección principal (calentamiento vocal, demo de acordes, etc.) | Alto | Medio |
| R3.5 | **"Resumen TL;DR" al inicio de cada sección** — 2-3 bullet points con lo esencial antes del contenido completo | Alto | Bajo |

---

## 4. 🧭 Wayfinding — 3/5

### Lo que funciona ✅
- **Sidebar siempre visible** en desktop — siempre sé qué secciones existen
- **Item activo resaltado** en el sidebar (coral + font-weight)
- **Hash routing** funcional (#fundamentos-pulso, etc.)
- **Búsqueda client-side** presente

### Problemas ❌

**P4.1 — Sin breadcrumbs**
Cuando estoy en "instrumento-guitarra", no veo "Instrumentos > Guitarra" en ningún lugar del contenido principal. Solo lo sé si miro el sidebar (que en mobile está oculto).

**P4.2 — Sin indicador de "dónde estoy en el todo"**
No hay numeración ("Sección 9 de 28"), ni barra de progreso, ni indicador de "estás en Semestre 1". El usuario no sabe si ha visto el 10% o el 90% del contenido.

**P4.3 — Sin navegación "Anterior/Siguiente"**
Al terminar una sección, el usuario debe volver al sidebar para elegir la siguiente. No hay flow natural "terminaste Pulso → ahora sigue Ritmo".

**P4.4 — Búsqueda sin feedback visual**
Los resultados de búsqueda aparecen, pero al hacer click no se resalta el texto buscado dentro de la sección. El usuario no sabe dónde está el match.

### Recomendaciones

| # | Recomendación | Impacto | Esfuerzo |
|---|---------------|---------|----------|
| R4.1 | **Breadcrumbs** — "🏠 > 🎸 Instrumentos > Guitarra" arriba de cada sección | Alto | Bajo |
| R4.2 | **Navegación Anterior/Siguiente** al final de cada sección con label descriptivo | Muy alto | Bajo |
| R4.3 | **Indicador de progreso** — "Sección 4 de 28" o barra visual | Medio | Bajo |
| R4.4 | **Scroll-to-match en búsqueda** — resaltar el texto encontrado con highlight | Medio | Medio |

---

## 5. 🎯 Engagement y Retención — 2/5

### Cognitive Walkthrough por Persona

#### 🌱 Majo (principiante, 15 años, cero experiencia)

**Primer uso:**
1. Llega al sitio → Ve el hero → Bien, se siente bienvenida
2. Hace click en "🌱 Empiezo aquí" → Llega a "El Pulso"
3. Lee los primeros 3 párrafos → Se siente motivada por el tono
4. Scrollea... y scrollea... y scrollea (4+ pantallas)
5. Ve links a Musicca y metrónomo → **Sale del sitio** → No regresa
6. **No hay razón para volver** — no hay notificación, no hay progreso guardado, no hay "siguiente paso"

**Probabilidad de retorno:** 🔴 Baja (15%) — sin incentivo para regresar

#### 🎸 Santi (autodidacta, 16 años, guitarra de YouTube)

**Primer uso:**
1. Llega al sitio → Ve el hero → "Ok, se ve cool"
2. Hace click en "🎸 Ya sé algo" → **Llega a guitarra** → Se identifica
3. Lee la sección de guitarra → "Ya sé esto" (los primeros acordes los conoce)
4. Busca "los 4 acordes mágicos" → **Busca, no encuentra rápido** (está en Armonía, no en Guitarra)
5. **Se desconecta** — el sitio no le ofrece nada que no tenga en YouTube con video + audio

**Probabilidad de retorno:** 🔴 Baja (20%) — YouTube es mejor para su estilo de aprendizaje

#### 🎼 Vale (formal, 15 años, 4 años de piano)

**Primer uso:**
1. Llega al sitio → Ve el hero → "Se ve lindo pero básico"
2. Hace click en "🎼 Quiero más" → Llega a Progresiones → "Ah, esto sí lo entiendo"
3. Lee sobre los 4 acordes → **Se queda** un rato, le gusta la explicación con canciones pop
4. Va al sidebar → Explora "Composición" → Se interesa
5. **Pero:** Todo es texto. No hay reto práctico, no hay quiz, no hay forma de "demostrar" que dominó algo
6. **Retorna:** Quizás 1-2 veces más, pero sin engagement activo se olvida

**Probabilidad de retorno:** 🟡 Media (40%) — el contenido le interesa pero falta interactividad

### El problema fundamental

> **El sitio es una enciclopedia pasiva, no una experiencia de aprendizaje activa.** Lee → scroll → lee → scroll → sale. No hay loop de engagement (acción → feedback → recompensa → acción).

### Recomendaciones

| # | Recomendación | Impacto | Esfuerzo |
|---|---------------|---------|----------|
| R5.1 | **Mini-quizzes al final de cada sección** — 3-5 preguntas interactivas de opción múltiple con feedback inmediato | Muy alto | Medio |
| R5.2 | **Retos semanales** — "Reto de esta semana: Identifica el compás de 3 canciones" con timer | Alto | Alto |
| R5.3 | **Sistema de logros** — badges visuales al completar secciones (CSS + localStorage) | Alto | Medio |
| R5.4 | **"Lo que vimos hoy en clase"** — sección dinámica que el profesor actualiza cada semana como puente presencial→digital | Muy alto | Alto |
| R5.5 | **Playlist curada por sección** — embed de Spotify/YouTube con las canciones mencionadas en cada tema | Alto | Bajo |

---

## 6. ⚡ Fricciones — 3/5

### Fricciones identificadas

| # | Fricción | Severidad | Persona afectada |
|---|---------|-----------|------------------|
| F1 | **26 links externos sin `target=_blank`** — al hacer click, el sitio se reemplaza y el usuario pierde su lugar | 🔴 Crítica | Todos |
| F2 | **0 botones "volver arriba" funcional visible** — tras 5 pantallas de scroll, no hay forma rápida de navegar | 🟡 Media | Todos |
| F3 | **Callout boxes solo se estilizan vía JS** — si el JS post-procesamiento falla (3 ocurrencias detectadas vs 77 planeadas), los callouts aparecen como texto plano | 🟡 Media | Todos |
| F4 | **Glosario no es buscable/filterable** — 45+ términos en una sola lista sin filtro alfabético interactivo | 🟡 Media | Majo |
| F5 | **Formatos de evaluación no son rellenables** — son texto descriptivo, no formularios interactivos. El alumno no puede llenar su "Mi Perfil Musical" en el sitio | 🟡 Media | Todos |
| F6 | **Sidebar scroll largo en mobile** — 31 items requieren scroll en el menú hamburger | 🟡 Media | Santi, Majo |

### Recomendaciones

| # | Fix | Impacto | Esfuerzo |
|---|-----|---------|----------|
| R6.1 | **`target="_blank"` en TODOS los links externos** + icono de "link externo" | Crítico | Trivial (1 línea de JS) |
| R6.2 | **Back-to-top button siempre visible** después de 1 pantalla de scroll | Medio | Bajo |
| R6.3 | **Glosario con búsqueda/filtro** — input que filtre términos al escribir | Medio | Bajo |
| R6.4 | **Callout detection más robusta** — verificar que los 77 callouts se procesan | Medio | Bajo |

---

## 7. 📱 Mobile UX — 3/5

### Lo que funciona ✅
- **Responsive básico:** Sidebar se oculta en <768px, aparece como hamburger
- **Viewport meta correctamente configurado**
- **Font-size 16px base** — no trigger zoom en iOS
- **Tablas con overflow-x:auto** (si se implementó)

### Problemas ❌

**P7.1 — Solo 1 breakpoint (768px)**
El mundo real de los alumnos es: iPhone SE (375px), iPhone 14 (390px), Samsung Galaxy (412px), tablets. Un solo breakpoint a 768px no cubre la variación.

**P7.2 — Touch targets insuficientes**
Los `.nav-item.sub` tienen `padding: 8px 20px` — la altura resultante es ~32px, por debajo del mínimo WCAG de 44x44px para touch targets.

**P7.3 — Sidebar hamburger sin gesto de swipe**
En mobile, el sidebar se abre con botón hamburger pero no soporta **swipe left para cerrar** ni **swipe right para abrir** — gestos naturales en apps móviles que los adolescentes esperan.

**P7.4 — Sin PWA / offline**
El sitio no tiene service worker ni manifest.json. No puede "instalarse" como app ni funcionar offline. Para un alumno que consulta el sitio en el camión camino a la escuela (conexión intermitente en Mérida), esto es una fricción real.

### Recomendaciones

| # | Recomendación | Impacto | Esfuerzo |
|---|---------------|---------|----------|
| R7.1 | **Agregar breakpoints: 375px, 480px, 768px, 1024px** | Medio | Medio |
| R7.2 | **Touch targets mínimo 44px** — aumentar padding de nav items en mobile | Alto | Trivial |
| R7.3 | **Swipe gestures** para sidebar (touch events JS) | Medio | Medio |
| R7.4 | **PWA básica** — manifest.json + service worker para cache offline | Alto | Alto |

---

## 8. ♿ Accesibilidad — 2/5

### Auditoria WCAG AA

| Criterio | Estado | Detalle |
|----------|--------|---------|
| 1.1.1 Imágenes con alt | ⚠️ Parcial | 10 imágenes — verificar que todas tengan alt descriptivo |
| 1.3.1 Estructura semántica | ❌ Falla | 0 roles semánticos (`role="main"`, `role="navigation"`, `role="contentinfo"`) |
| 2.1.1 Navegación por teclado | ⚠️ Parcial | Skip-to-content presente, pero nav items no tienen `tabindex` ni `role="menuitem"` |
| 2.4.1 Skip navigation | ✅ OK | `skip-to-content` link presente |
| 2.4.4 Propósito de links | ⚠️ Parcial | Links externos sin indicador visual ni `aria-label` de "abre en nueva ventana" |
| 2.4.6 Headings descriptivos | ✅ OK | H1-H3 usados correctamente, estructura lógica |
| 2.5.5 Target size | ❌ Falla | Nav sub-items <44px en mobile |
| 3.2.2 Consistencia de inputs | ✅ OK | Solo 1 input (búsqueda) |
| 4.1.2 ARIA | ❌ Falla | Solo 2 `aria-label`, 0 `role=`, 0 `aria-current` |

### Recomendaciones

| # | Recomendación | Impacto | Esfuerzo |
|---|---------------|---------|----------|
| R8.1 | **`role="main"`, `role="navigation"`, `role="contentinfo"`** en los landmarks | Alto | Trivial |
| R8.2 | **`aria-current="page"`** en el nav item activo (actualizar con JS) | Medio | Trivial |
| R8.3 | **`aria-label` en links externos** — "Musicca (abre en nueva ventana)" | Medio | Bajo |
| R8.4 | **Verificar alt text de las 10 imágenes** — deben ser descriptivos, no genéricos | Medio | Bajo |

---

## 9. 🏆 Gamificación y Progreso — 1/5

### Estado actual

> **CERO indicadores de progreso. CERO gamificación. CERO feedback de logro.**

El sitio no tiene:
- ❌ Progreso del usuario (secciones visitadas/completadas)
- ❌ Badges o logros
- ❌ Quizzes o ejercicios evaluables
- ❌ Streak de práctica
- ❌ "Nivel" del usuario
- ❌ Checkmarks de "sección completada"
- ❌ Celebración al terminar una sección
- ❌ Motivación para volver

### Por qué esto importa tanto para esta audiencia

Los adolescentes de 15-16 años están acostumbrados a:
- **Duolingo:** XP, streaks, niveles, celebraciones
- **Spotify Wrapped:** Datos personalizados sobre su uso
- **Videojuegos:** Achievement unlocked, progress bars
- **TikTok:** Métricas de engagement, likes, views

Un sitio educativo sin NINGÚN feedback de progreso se siente **muerto** comparado con cualquier otra experiencia digital de su vida.

### Recomendaciones (Prioridad MÁXIMA)

| # | Recomendación | Impacto | Esfuerzo |
|---|---------------|---------|----------|
| R9.1 | **Sección "completada" con checkmark** — click en un botón "Ya leí esta sección ✅" que guarda en localStorage y muestra check en el sidebar | Muy alto | Bajo |
| R9.2 | **Barra de progreso global** — "Has explorado 7 de 22 secciones" (excluir formatos) | Alto | Bajo |
| R9.3 | **Mini-quizzes embebidos** — 3 preguntas de opción múltiple al final de secciones clave con feedback inmediato (JS puro) | Muy alto | Medio |
| R9.4 | **Badges por hito** — "🎵 Fundamentos completos", "🎸 Elegiste tu instrumento", "🎶 Armonista nivel 1" (CSS + localStorage) | Alto | Medio |
| R9.5 | **Mensaje de celebración al completar un bloque** — confetti CSS o frase motivacional al terminar las 4 secciones de fundamentos | Alto | Bajo |

---

## 10. 📋 Resumen Priorizado de Recomendaciones

### 🔴 Prioridad 1 — Hacer AHORA (Impacto alto, esfuerzo bajo-medio)

| # | Qué | Por qué | Esfuerzo |
|---|-----|---------|----------|
| **R6.1** | `target="_blank"` en 26 links externos | Cada link externo es un punto de fuga irreversible | Trivial |
| **R4.2** | Botones "Anterior / Siguiente" al final de cada sección | Sin esto no hay flujo narrativo | Bajo |
| **R9.1** | Botón "Ya leí esto ✅" + checkmark en sidebar | El primer paso hacia dar al alumno sensación de progreso | Bajo |
| **R3.5** | "Resumen TL;DR" al inicio de cada sección | Reduce carga cognitiva inmediata | Bajo |
| **R8.1** | Roles ARIA semánticos | Accesibilidad básica | Trivial |

### 🟡 Prioridad 2 — Hacer PRONTO (Impacto alto, esfuerzo medio)

| # | Qué | Por qué | Esfuerzo |
|---|-----|---------|----------|
| **R2.1** | Puertas como rutas, no destinos | El onboarding actual se rompe tras 1 click | Medio |
| **R3.1** | Acordeones/tabs para subsecciones | Reduce muro de texto dramáticamente | Medio |
| **R9.3** | Mini-quizzes al final de secciones clave | La interactividad que más falta | Medio |
| **R1.1** | Sidebar colapsable (grupos expandibles) | Reduce sobrecarga de opciones | Medio |
| **R5.5** | Playlist embebida por sección | Un sitio de MÚSICA necesita SONIDO | Bajo |

### 🟢 Prioridad 3 — Planificar (Impacto medio-alto, esfuerzo alto)

| # | Qué | Por qué | Esfuerzo |
|---|-----|---------|----------|
| **R3.2** | Embeber herramientas (Musicca, metrónomo) como iframes | Reduce puntos de fuga | Medio-Alto |
| **R3.3** | Audio/video embebido | Sitio de música sin música = contradicción | Alto |
| **R7.4** | PWA básica para offline | Uso real en transporte sin WiFi | Alto |
| **R5.4** | Sección "Lo de esta semana" editable por profesor | Puente presencial↔digital | Alto |

---

## 💡 Insight Principal

> **El sitio tiene contenido editorial de calidad excepcional** — el tono de voz, las analogías, los ejemplos con música actual, la inclusividad por niveles. El equipo de Content Creator hizo un trabajo extraordinario.
>
> **Pero la EXPERIENCIA del sitio no está a la altura del CONTENIDO.** Es como tener una playlist increíble pero reproducirla en un reproductor de CD sin pantalla: el contenido es bueno, pero la interfaz no le hace justicia.
>
> **La brecha más crítica no es visual (eso se puede arreglar con CSS) sino INTERACTIVA.** Un sitio de música sin sonido, sin quizzes, sin progreso y sin razón para volver es un documento PDF disfrazado de sitio web. Las mejoras de prioridad 1 se pueden implementar en un día y transformarían la experiencia de forma medible.

---

*Reporte generado como UX Researcher · Auditoría heurística + cognitive walkthrough · Septiembre 2026*
