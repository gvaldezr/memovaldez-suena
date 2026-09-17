# 🎵 Suena — Tu Espacio Musical

> Sitio web complementario para el Taller de Música · Bachillerato UADY · MEFI

## ¿Qué es Suena?

**Suena** es un sitio web público que complementa las clases presenciales del Taller de Música de primer grado de bachillerato en la Universidad Autónoma de Yucatán (UADY), en el marco del Modelo Educativo para la Formación Integral (MEFI).

El sitio ofrece formación musical básica para nivelar un grupo heterogéneo de estudiantes — desde quienes nunca han tocado un instrumento hasta quienes tienen formación académica.

## 🎯 Audiencia

- Adolescentes de 15-16 años, 1er grado de bachillerato
- Nivel musical heterogéneo: académicos, autodidactas, principiantes
- Dispositivo principal: celular

## 🏗️ Estructura del Proyecto

```
memovaldez-suena/
├── README.md                          ← Este archivo
├── .gitignore
│
├── site/                              ← 🌐 SITIO WEB (lo que se publica)
│   └── index.html                     ← HTML self-contained (~1 MB)
│
├── docs/                              ← 📚 DOCUMENTACIÓN DEL PROYECTO
│   ├── 01_brief_estrategico/          ← Fase 1: Brief, personas, Go/No-Go
│   ├── 02_base_conocimiento/          ← Fase 2: Literatura, frameworks, fuentes
│   ├── 03_diseno_curricular/          ← Fase 3: Plan, cartas, secuencias, rúbricas
│   ├── 04_contenido_curado/           ← Fase 4: Mapa de fuentes, arco narrativo
│   ├── 05_produccion_contenido/       ← Fase 5: Textos y formatos del sitio
│   │   ├── textos/                    ← 22 textos Markdown
│   │   └── formatos/                  ← 6 formatos de evaluación
│   └── 06_assets/                     ← Fase 6: Brand guide, imágenes, prompts
│
├── auditorias/                        ← 🔍 REPORTES DE AUDITORÍA
│   ├── v1/                            ← Primera auditoría (5 expertos)
│   ├── v2/                            ← Re-auditoría post-reconstrucción
│   └── v2.1/                          ← Auditoría post-correcciones (en proceso)
│
└── specs/                             ← 📐 ESPECIFICACIONES TÉCNICAS
    ├── architecture_spec.md
    ├── design_system_v2.md
    └── whimsy_recipe.md
```

## 🚀 Cómo usar

### Ver el sitio localmente
```bash
open site/index.html
```
El archivo es self-contained — funciona sin servidor web, sin dependencias, offline (excepto Google Fonts).

### Publicar en GitHub Pages
1. Push a GitHub
2. Settings → Pages → Source: main branch, /site folder
3. El sitio estará en `https://[usuario].github.io/memovaldez-suena/`

## 📊 Métricas del Proyecto

| Métrica | Valor |
|---------|-------|
| Fases del pipeline | 7 de 7 completadas |
| Archivos generados | 75+ |
| Secciones del sitio | 28 |
| Palabras de contenido | ~35,000 |
| Fuentes verificadas | 31 (URLs confirmadas) |
| Imágenes ilustrativas | 10 |
| Formatos de evaluación | 6 |
| Rondas de auditoría | 3 (15 reportes de expertos) |
| Score de diseño | v1: 3.0 → v2: 3.7 → v2.1: ~4.2 |

## 🎨 Identidad Visual

- **Nombre:** Suena — Tu Espacio Musical
- **Primary:** Coral Cálido `#E8614D`
- **Secondary:** Azul Profundo `#2D3A4A`
- **Accent:** Verde Menta `#2EC4A0`
- **Headings:** Nunito
- **Body:** Inter
- **Código/Cifrado:** JetBrains Mono

## 📋 Marco Curricular

- **Asignaturas:** Sem 1 "Desarrollo físico y artístico" + Sem 2 "Creatividad en movimiento"
- **Sesiones:** 14 por semestre, 28 total
- **Duración:** 90 min/sesión, presencial, semanal
- **Evaluación:** 70% proceso / 30% producto
- **Presentaciones:** Diciembre (Navidad) + Junio (temáticas varias)

## 🛠️ Tecnología

- HTML5 self-contained (sin framework)
- CSS con 80+ custom properties (design tokens)
- JavaScript vanilla (navegación, acordeones, search, dark mode, progress tracking, confetti, easter eggs)
- Google Fonts CDN (Nunito, Inter, JetBrains Mono)
- Imágenes JPEG base64 inline (~1 MB total)
- Mobile-first, 3 breakpoints (480px, 768px, 1200px)

## 📄 Licencia

Contenido educativo para uso interno del Taller de Música, Bachillerato UADY.
